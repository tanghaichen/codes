1、使用easypoi时，背景色设置不生效：
  ```
             CellStyle cellStyle = workbook.createCellStyle();//创建单元格样式
             cellStyle.setAlignment(HorizontalAlignment.CENTER);//水平居中
             
             
             cellStyle.setFillForegroundColor(IndexedColors.CORNFLOWER_BLUE.index);//设置背景色
             cellStyle.setFillPattern(FillPatternType.SOLID_FOREGROUND);//设置背景色填充方式
             Font font = workbook.createFont();//创建字体且使其生效
             font.setFontName("黑体");
             font.setBold(true);
             font.setFontHeightInPoints((short) 16);//设置字体大小
             cellStyle.setFont(font);
             
             CellRangeAddress craOne = new CellRangeAddress(0, 0, 0, listMap.size());//合并单元格
             workbook.getSheetAt(0).addMergedRegion(craOne);
             Sheet sheetAt = workbook.getSheetAt(0);//获取sheet页和单元格
             Cell cell = sheetAt.getRow(0).getCell(0);
             cell.setCellStyle(cellStyle); //将单元格设置样式使其生效
   ```
   2、使用spirt进行excel导出png时，直接使用  冰兰科技[https://www.e-iceblue.cn/spirexlsjavaconversion/convert-excel-to-pdf-using-java.html]使用其进行转换时，图片边距问题
       可优先将其设置边距，之后再进行图片转换，即可实现。
       ```
            PageSetup pageSetup = worksheet.getPageSetup();
            pageSetup.setTopMargin(0);
            pageSetup.setBottomMargin(0);
            pageSetup.setLeftMargin(0);
            pageSetup.setRightMargin(0);
       ```
