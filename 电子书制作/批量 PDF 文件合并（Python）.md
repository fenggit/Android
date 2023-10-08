# 批量 PDF 文件合并（Python）



```
import os
from PyPDF2 import PdfMerger

# 指定输入文件夹路径和输出文件路径
input_folder = '/Users/xx/xxx'       # 输入文件夹路径
output_folder = '/Users/xxx/pdf2/'   # 输出文件夹路径

# 创建输出文件夹
if not os.path.exists(output_folder):
    os.makedirs(output_folder)

# 获取输入文件夹中的所有PDF文件，并按照文件名排序
input_files = [file for file in os.listdir(input_folder) if file.lower().endswith('.pdf')]
input_files.sort()  # 按文件名排序

# 构建输出文件路径（文件夹名 + .pdf）
output_filename = os.path.basename(os.path.abspath(input_folder)) + '.pdf'
output_path = os.path.join(output_folder, output_filename)

# 合并PDF文件的函数
def merge_pdfs(input_files, output_path):
    merger = PdfMerger()

    for pdf_file in input_files:
        pdf_path = os.path.join(input_folder, pdf_file)
        merger.append(pdf_path)

    with open(output_path, 'wb') as output_file:
        merger.write(output_file)

# 合并PDF文件
merge_pdfs(input_files, output_path)
print(f'Merged PDFs saved as: {output_path}')
```

