# 一、元素及结构

## 1、文件结构

    presentataion ppt文件
    
    presentation.slides 幻灯片集合 iterable --> slide 幻灯片
    
    slide.shapes 窗格集合 iterable --> shape 窗格
    
    shape.name 窗格名称
    
## 2、文本结构
    
    shape.text_frame 文本窗
    
    text_frame.text 文本窗的所有文字
    
    text_frame.paragraphs 段落集合 iterable --> paragraph 段落
    
    paragraph.runs 文本单位集合 iterable --> run 文本单位
    
    run.text 一个文本单位的文字
    
## 3、图表结构
    
    shape.chart 图表窗
    
    chart.data 图表数据
    
    chart.chart_title 图表标题
    
## 4、表格结构

    shape.table 表格窗
    
    table.cell(i, j) 单元格(行, 列)
    
# 二、各元素应用

## 1、文件

    prs = pptx.Presentation("/.pptx") 读取ppt文件
    
    for slide in prs.slides:
    
        shapes = {}
        
        for shape in slide.shapes:
        
            shapes[shape.name] = shape 构成{"窗格名称": 窗格对象}的字典
            
    if "窗格名称" in shapes: 通过对幻灯片独有的窗格名称的判断，可找到对应的幻灯片并进行后续操作
    
    > from pptx.enum.shapes import MSO_AUTO_SHAPE_TYPE
    
    slide.shapes.add_shape(MSO_AUTO_SHAPE_TYPE.UP_ARROW, left, top, width, height) 新增图形(形状，与左边缘距离，与顶边缘距离，宽度，高度)
     
## 2、文本

    shapes['窗格名称'].text_frame.text = '' 清空原有文本窗
    
    > from pptx.enum.text import PP_PARAGRAPH_ALIGNMENT
    
    shapes['窗格名称'].text_frame.paragraphs[0].alignment = PP_PARAGRAPH_ALIGNMENT 段落水平居中
    
    > from pptx.enum.text import MSO_VERTICAL_ANCHOR
    
    shapes['窗格名称'].text_frame.vertical_anchor = MSO_VERTICAL_ANCHOR.MIDDLE 垂直居中
    
    shapes['窗格名称'].text_frame.paragraphs[0].font.size = Pt(12) 整个段落12号字体
    
    shapes['窗格名称'].text_frame.paragraphs[0].font.bold = True 整个段落加粗
    
    > from pptx.dml.color import RGBColor
    
    shapes['窗格名称'].text_frame.paragraphs[0].font.color.rgb = RGBColor(62, 100, 125) 设置文字RGB颜色
    
    shapes['窗格名称'].fill.solid() 窗格填充初始化（存疑）
    
    shapes['窗格名称'].fill.fore_color.rgb = RGBColor(255, 255, 255) 设置窗格填充颜色
    
    shapes['窗格名称'].line.color.rgb = RGBColor(255, 255, 255) 设置窗格边框颜色
    
    shapes['窗格名称'].text_frame.paragraphs[0].name = '微软雅黑' 整个段落字体为微软雅黑，但不包含中文字符
    
    shapes['窗格名称'].text_frame.paragraphs[0].add_run() 新增文本单位，文本单位字体、内容设置格式与段落相同
    
    > import pptx_ea_font
    
    pptx_ea_font.set_font(shapes['窗格名称'].text_frame.paragraphs[0].runs[i], '微软雅黑') 设置第i个文本单位的中文字为微软雅黑
    
## 图表

    > form pptx.chart.data import ChartData
    
    chart_data = ChartData() 初始化
    
    chart_data.categories = [] 设置图表数据的横坐标
    
    chart_data.add_series('列名', []) 设置图表数据的列值
    
    shapes['窗格名称'].chart.replace_data(chart_data) 用chart_data替换原图表数据
    
## 表格
    
    for j in range(0, y):
    
        for i in range(0, x):
        
            shapes['窗格名称'].cell.text = value 逐格赋值
            
            shapes['窗格名称'].cell.fill.solid() 单元格填充初始化
            
            shapes['窗格名称'].cell.fill.fore_color.rgb = RGBColor(221, 163, 167) 单元格填充颜色
            
            shapes['窗格名称'].cell.textframe. 字体设置与文本窗相同
             
    表格起始格为cell(0, 0)
