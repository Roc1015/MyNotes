# java_Tool

## 一.HuTool



## 简要说明：

**下面的工具主要是对Excel进行操作，数据的导入导出。java的IO同样可以做类似的事情，但是底层实现远不如直接调用第三方的工具类实现简单方便，肯定是能懒则懒。**

## 二.EasyExcel

### 1.EasyExcel是什么？

**官方地址：https://www.yuque.com/easyexcel/doc/easyexcel**

### 2.为什么要使用EasyExcel？

### 3.集成EasyExcel

## 三.POI(Apache POI)

### 1.POI是什么？

```xml
Apache POI 简介是用Java编写的免费开源的跨平台的 Java API，Apache POI提供API给Java程式对Microsoft Office（Excel、WORD、PowerPoint、Visio等）格式档案读和写的功能。POI为“Poor Obfuscation Implementation”的首字母缩写，意为“可怜的模糊实现”。
```

### 2.POI的基本功能

**Apache POI常用的类**

```xml
HSSF － 提供读写Microsoft Excel XLS格式档案的功能。
XSSF － 提供读写Microsoft Excel OOXML XLSX格式档案的功能。
HWPF － 提供读写Microsoft Word DOC97格式档案的功能。
XWPF － 提供读写Microsoft Word DOC2003格式档案的功能。
HSLF － 提供读写Microsoft PowerPoint格式档案的功能。
HDGF － 提供读Microsoft Visio格式档案的功能。
HPBF － 提供读Microsoft Publisher格式档案的功能。
HSMF － 提供读Microsoft Outlook格式档案的功能。
```

Excel 2003表格最大行数：65536

Excel 2007表格最大行数：无限制

### 3.SpringBoot集成POI进行写文件

#### 1.新建SpringBoot项目导入依赖

```xml
<dependencies>
    <!--xls(03)-->
    <dependency>
        <groupId>org.apache.poi</groupId>
        <artifactId>poi</artifactId>
        <version>3.9</version>
    </dependency>
    <!--xlsx(07)-->
    <dependency>
        <groupId>org.apache.poi</groupId>
        <artifactId>poi-ooxml</artifactId>
        <version>3.9</version>
    </dependency>
    <!--日期格式化工具-->
    <dependency>
        <groupId>joda-time</groupId>
        <artifactId>joda-time</artifactId>
        <version>2.10.1</version>
    </dependency>
    <!--test-->
    <dependency>
        <groupId>junit</groupId>
        <artifactId>junit</artifactId>
        <version>4.12</version>
    </dependency>
</dependencies>

```

#### 2.认清表格+03版本的.xls表格和07版本的.xlsx表格

![image-20210125225520375](../imgs/image-20210125225520375.png)

识别出表格中的几个对象

工作簿

工作表

行

列

#### 3.测试03版本的简单创建工作簿

```java
//import相关依赖
public class ExcelWriteTest03 {

    String Path = "D:\\MyDemos\\RD\\java\\demos\\excelStudy";

    @Test
    public void testWrite03() throws IOException {
        //1.创建一个工作簿
        HSSFWorkbook workbook = new HSSFWorkbook();
        //2.创建一个工作表
        HSSFSheet sheet = workbook.createSheet();
        //3.创建第一行
        Row row1 = sheet.createRow(0);
        //4.创建第一列
        Cell cell0101 = row1.createCell(0);
        //4.创建第二列
        Cell cell0102 = row1.createCell(1);
        //5.放入数据
        cell0101.setCellValue("信息");
        cell0102.setCellValue("这是POI的一节课");

        //创建第二行
        HSSFRow row2 = sheet.createRow(1);
        //创建第二行的第一列和第二列，且向第二的第一列和第二列放入日期格式的值
        Cell cell0201 = row2.createCell(0);
        Cell cell0202 = row2.createCell(1);
        cell0201.setCellValue("时间");
        String dateTime = new Date().toString();
        cell0202.setCellValue(dateTime);

        //生成一张表(IO文件流) 03版本的后缀为.xls
        //代码操作文件依旧是通过IO操作，new一个新的IO文件流，且使用完IO流之后关闭
        //使用IO流的过程中不断抛出异常
        FileOutputStream fileOutputStream = new FileOutputStream(Path + "POI的第一张表03.xls");
        workbook.write(fileOutputStream);
        fileOutputStream.close();
    }
}
```

![image-20210125235555704](../imgs/image-20210125235555704.png)

![image-20210125235616529](../imgs/image-20210125235616529.png)

#### 4.测试07版本的简单创建工作簿

```java
public class ExcelWriteTest07 {

    String Path = "D:\\MyDemos\\RD\\java\\demos\\excelStudy";

    @Test
    public void testWrite07() throws IOException {
        //1.创建一个工作簿
        XSSFWorkbook workbook = new XSSFWorkbook();
        //2.创建一个工作表
        XSSFSheet sheet = workbook.createSheet();
        //3.创建第一行
        Row row1 = sheet.createRow(0);
        //4.创建第一列
        Cell cell0101 = row1.createCell(0);
        //4.创建第二列
        Cell cell0102 = row1.createCell(1);
        //5.放入数据
        cell0101.setCellValue("信息");
        cell0102.setCellValue("这是POI的一节课");

        //创建第二行
        Row row2 = sheet.createRow(1);
        //创建第二行的第一列和第二列，且向第二的第一列和第二列放入日期格式的值
        Cell cell0201 = row2.createCell(0);
        Cell cell0202 = row2.createCell(1);
        cell0201.setCellValue("时间");
        String dateTime = new Date().toString();
        cell0202.setCellValue(dateTime);

        //生成一张表(IO文件流) 07版本的后缀为.xlsx
        //代码操作文件依旧是通过IO操作，new一个新的IO文件流，且使用完IO流之后关闭
        //使用IO流的过程中不断抛出异常
        FileOutputStream fileOutputStream = new FileOutputStream(Path + "POI的第一张表.xlsx");
        workbook.write(fileOutputStream);
        fileOutputStream.close();
    }
}
```

![image-20210125235643983](../imgs/image-20210125235643983.png)

![image-20210125235707744](../imgs/image-20210125235707744.png)

#### 5.测试03数据批量导入！

```java
public class BigDataWrite03 {

    String Path = "D:\\MyDemos\\RD\\java\\demos\\excelStudy";

    @Test
    public void BigDataWriteTest03() throws IOException {
        //获取程序开始时系统的时间且转换成秒
        long begin = System.currentTimeMillis();

        //创建一个工作簿
        HSSFWorkbook workbook03 = new HSSFWorkbook();
        //创建一个工作表
        HSSFSheet sheet = workbook03.createSheet();

        //写入数据
        //for循环写入
        //循环创建65336行
        for (int rowNum = 0;rowNum<65536;rowNum++){
            HSSFRow row = sheet.createRow(rowNum);
            for(int cellNum = 0;cellNum<10;cellNum++){
        //每行循环创建10列且填入数据
                HSSFCell cell = row.createCell(cellNum);
                cell.setCellValue(cellNum);
            }
        }
        //创建成功后
        System.out.println("over");
        //输出数据到文件中
        FileOutputStream fileOutputStream = new FileOutputStream(Path + "BigDataWriteTest03.xls");
        workbook03.write(fileOutputStream);
        fileOutputStream.close();

        //获取程序结束时系统的时间且转换成秒
        long end = System.currentTimeMillis();
        //计算前后总计花费多长时间
        System.out.println((double) (end-begin)/1000);
    }
}
```

![image-20210125235730703](../imgs/image-20210125235730703.png)

![image-20210126000347938](../imgs/image-20210126000347938.png)

**使用时间为：**

![image-20210126000411392](../imgs/image-20210126000411392.png)

#### 6.测试07数据批量导入！

```java
public class BigDataWrite07 {

    String Path = "D:\\MyDemos\\RD\\java\\demos\\excelStudy";

    @Test
    public void BigDataWriteTest07() throws IOException {
        //获取程序开始时系统的时间且转换成秒
        long begin = System.currentTimeMillis();

        //创建一个工作簿
        XSSFWorkbook workbook07 = new XSSFWorkbook();
        //创建一个工作表
        XSSFSheet sheet = workbook07.createSheet();

        //写入数据
        //for循环写入
        //同样循环创建65336行
        for (int rowNum = 0; rowNum < 65536; rowNum++) {
            XSSFRow row = sheet.createRow(rowNum);
            for (int cellNum = 0; cellNum < 10; cellNum++) {
                //每行循环创建10列且填入数据
                XSSFCell cell = row.createCell(cellNum);
                cell.setCellValue(cellNum);
            }
        }
        //创建成功后
        System.out.println("over");
        //输出数据到文件中
        FileOutputStream fileOutputStream = new FileOutputStream(Path + "BigDataWriteTest07.xlsx");
        workbook07.write(fileOutputStream);
        fileOutputStream.close();

        //获取程序结束时系统的时间且转换成秒
        long end = System.currentTimeMillis();
        //计算前后总计花费多长时间
        System.out.println((double) (end - begin) / 1000);
    }
}
```

![image-20210126000836877](../imgs/image-20210126000836877.png)

花费的时间为：

![image-20210126000903569](../imgs/image-20210126000903569.png)

相比之下花费的时间就更长了

但是07可以写更多的数据：测试写100000行10列数据花费多长的时间：

![image-20210126001123360](../imgs/image-20210126001123360.png)

![image-20210126001129592](../imgs/image-20210126001129592.png)

测试写1000000000行10列数据花费多长的时间：10亿行数据

![image-20210126001222242](../imgs/image-20210126001222242.png)

电脑资源使用情况：

![image-20210126001318810](../imgs/image-20210126001318810.png)

好吧，内存溢出······

![image-20210126001535984](../imgs/image-20210126001535984.png)

#### 7.解决07超大数据批量写入可能存在的内存溢出：SXSSF

```java
public class SuperDataWrite007 {

    String Path = "D:\\MyDemos\\RD\\java\\demos\\excelStudy";

    @Test
    public void SuperDataWrite007() throws IOException {
        //获取程序开始时系统的时间且转换成秒
        long begin = System.currentTimeMillis();

        //创建一个工作簿
        Workbook workbook007 = new SXSSFWorkbook();
        //创建一个工作表
        Sheet sheet = workbook007.createSheet();

        //写入数据
        //for循环写入
        //同样循环创建100000行
        for (int rowNum = 0; rowNum < 100000; rowNum++) {
            Row row = sheet.createRow(rowNum);
            for (int cellNum = 0; cellNum < 10; cellNum++) {
                //每行循环创建10列且填入数据
                Cell cell = row.createCell(cellNum);
                cell.setCellValue(cellNum);
            }
        }
        //创建成功后
        System.out.println("over");
        //输出数据到文件中
        FileOutputStream fileOutputStream = new FileOutputStream(Path + "SuperDataWrite007.xlsx");
        workbook007.write(fileOutputStream);
        fileOutputStream.close();
        //清除过程中产生的临时文件
        ((SXSSFWorkbook) workbook007).dispose();

        //获取程序结束时系统的时间且转换成秒
        long end = System.currentTimeMillis();
        //计算前后总计花费多长时间
        System.out.println((double) (end - begin) / 1000);
    }
}

```

![image-20210126002600450](../imgs/image-20210126002600450.png)

![image-20210126002550626](../imgs/image-20210126002550626.png)

![image-20210126002524170](../imgs/image-20210126002524170.png)

同样07的XSSF花费时间为：

![image-20210126002725003](../imgs/image-20210126002725003.png)

因此对比之下，可以选择SXSSF提高性能问题。

### 4.SpringBoot集成POI进行读文件













































































## POI和EasyExcel的相同点和区别

1.同样是第三方的组件对java操作Excel进行了优化。

2.实现的方式不同，两者存在性能上的问题：POI是将所有的数据一次性先写入内存，这样容易造成内存溢出，Easy Excel则是一条一条地读写数据，这样面对较大数据量时会存在时间成本问题。

**没有严格意义上的好坏，而是时间和空间的转换。**

![image-20210125221729809](../imgs/image-20210125221729809.png)