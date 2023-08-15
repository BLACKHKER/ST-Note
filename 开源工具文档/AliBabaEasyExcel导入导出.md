## Easy Excel 导出到Excel

### 一、导入依赖

```xml
<!-- EasyExcel -->
<dependency>
    <groupId>com.alibaba</groupId>
    <artifactId>easyexcel</artifactId>
    <version>2.1.6</version>
</dependency>
```







### 二、创建实体类

```java
@Data
@NoArgsConstructor
@AllArgsConstructor
@HeadRowHeight(30)  // 表头的行高
//@ContentRowHeight(10)   //内容的行高
public class Student {

    @ExcelProperty("ID")
    @ExcelIgnore    // 忽略
//    @ExcelProperty(value = "ID",index = 3)    // index 调整顺序，默认-1，按顺序排列,顺序编号从0开始
    private String id;

    @ExcelProperty("姓名")
    @ColumnWidth(20)
    private String name;

    @ExcelProperty("性别")
    private String gender;

    @ExcelProperty("生日")
    @ColumnWidth(40)
    @DateTimeFormat("yyyy-MM-dd")
    private Date birthday;
    
}
```







### 三、简单读

#### 编写读监听器

```java
import com.alibaba.excel.context.AnalysisContext;
import com.alibaba.excel.event.AnalysisEventListener;
import com.erp.purchase.entity.Student;

/**
 * @author PSY
 * @date 2023-05-12 15:17
 *
 * 读取文档的监听器类
 *
 */

public class StudentListener extends AnalysisEventListener<Student> {

    /**
     * 读监听器，每读一行内容，都会调用一次该对象额度invoke，在invoke可以操作使用读取到的数据
     * @param student   每次读取到的数据封装的对象
     * @param student   每次读取到的数据封装的对象
     * @param analysisContext
     */
    @Override
    public void invoke(Student student, AnalysisContext analysisContext) {
        // 将读取的结果输出到控制台，方便查看
        System.out.println("student = " + student);
    }

    /**
     * 读取完整个文档后调用的方法
     * @param analysisContext
     */
    @Override
    public void doAfterAllAnalysed(AnalysisContext analysisContext) {

    }
}
```





#### 编写测试类

##### <font color="red">注意：将需要读取的excel文件放在项目指定目录下，方便读取</font>

![image-20230512174739489](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202305230924310.png)![image-20230512174851552](https://typora-picture-zhao.oss-cn-beijing.aliyuncs.com/Typora/202305230924751.png)

```java
    /**
     * 读
     * 工作簿：一个excel文件就是一个工作簿
     * 工作表：一个工作簿中的每一个sheet就是一个工作表
     */
    @Test
    public void test01() {
        // 获得一个工作簿对象
        // pathName:要读的文件的路径
        // head:文件中每一行数据要存储到的实体的类型的class
        // readListener:读监听器，每读一行内容，都会调用一次该对象额度invoke，在invoke可以操作使用读取到的数据
        ExcelReaderBuilder readWorkBook = EasyExcel.read("学生.xlsx", Student.class, new StudentListener());
        // 获得一个工作表对象
        ExcelReaderSheetBuilder sheet = readWorkBook.sheet();
        // 读取工作表的内容
        sheet.doRead();
    }
```







### 四、简单写

#### 测试类

```java
    /**
     * 写
     */
    @Test
    public void test02() {

        // 工作簿对象
        // pathName:要写入的文件路径
        // head:封装写入的数据的实体的类型
        ExcelWriterBuilder writeWorkBook = EasyExcel.write("学生测试.xlsx", Student.class);
        // 工作表对象
        ExcelWriterSheetBuilder sheet = writeWorkBook.sheet();
        // 数据
        List<Student> students = initData();
        // 写
        sheet.doWrite(students);
    }

    // 生成数据
    private static List<Student> initData() {
        ArrayList<Student> students = new ArrayList<Student>();
        Student data = new Student();
        for (int i = 0; i < 10; i++) {
            data.setName("蜗牛01" + i);
            data.setBirthday(new Date());
            data.setGender("男");
            students.add(data);
        }
        return students;
    }
```







### 应用（数据生成Excel并下载到本地）

#### Requirements实体类

```java
import com.alibaba.excel.annotation.ExcelIgnore;
import com.alibaba.excel.annotation.ExcelProperty;
import com.alibaba.excel.annotation.format.DateTimeFormat;
import com.alibaba.excel.annotation.write.style.ColumnWidth;
import com.alibaba.excel.annotation.write.style.ContentRowHeight;
import com.alibaba.excel.annotation.write.style.HeadRowHeight;
import com.fasterxml.jackson.annotation.JsonFormat;
import lombok.AllArgsConstructor;
import lombok.Builder;
import lombok.Data;
import lombok.NoArgsConstructor;

import java.util.Date;

/**
 * @author PSY
 * @date 2023-05-09 17:47
 */
@Data
@NoArgsConstructor
@AllArgsConstructor
@Builder
@HeadRowHeight(30)  // 标题行高
@ContentRowHeight(20)    // 内容行高
public class Requirements {

    @ExcelIgnore
    private Integer id;         // 序号

    @ExcelProperty("单号")
    @ColumnWidth(30)
    private String rnum;        // 单号

    @ExcelProperty("客户")
    private String customer;    // 客户

    @ExcelProperty("部门")
    private String department;  // 部门

    @ExcelProperty("重量")
    private Double weight;      // 重量

    @ExcelProperty("数量")
    private Integer count;      // 数量

    @ExcelProperty("来货重量")
    @ColumnWidth(20)
    private Double inweight;    // 来货重量

    @ExcelProperty("来货数量")
    @ColumnWidth(20)
    private Integer incount;    // 来货数量

    @ExcelProperty("制单人")
    private String creator;     // 制单人

    @ExcelProperty("制单时间")
    @ColumnWidth(30)    // 表格数据宽度
    @JsonFormat(pattern = "yyyy-MM-dd HH:mm:ss")   // 数据时间格式
    @DateTimeFormat("yyyy-MM-dd HH:mm:ss")  // easyExcel时间格式
    private Date createtime;   // 制单时间

    @ExcelProperty("状态")
    private String status;      // 状态

}
```





#### 接口

```java
    /**
     * 导出需求单
     */
    @GetMapping("/exportRequirementsList")
    public void exportRequirementsList(HttpServletResponse response) throws IOException {
        response.setContentType("application/vnd.ms-excel");
        response.setCharacterEncoding("utf-8");
        String fileName = URLEncoder.encode("需求单","UTF-8").replaceAll("\\+","%20");
        // 文件名后添加自定义时间戳
        SimpleDateFormat dateFormat = new SimpleDateFormat("yyyyMMddHHmmss");
        String times = dateFormat.format(new Date());
        // 指定使用附件的形式下载excel文件
        response.setHeader("Content-disposition","attachment;filename=" + fileName + times + ".xlsx");
        EasyExcel.write(response.getOutputStream(),Requirements.class).excelType(ExcelTypeEnum.XLSX).sheet("需求单").doWrite(requirementsService.exportRequirementsList());
    }
```

