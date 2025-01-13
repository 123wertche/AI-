# AI-
TEST
<script src="https://gist.github.com/lanesky/6092906644c36d16ad39df3ac6d623d2.js">
  '''
convert.py 是一个脚本，用于读取 folder_path 的子文件夹中源文件和目标文件的内容
并将它们合并到一个数据集中。源文件是输入字段，目标文件是输出字段。
详情请参照 youtube 影片：https://youtu.be/Tq6qPw8EUVg
'''
导入操作系统
导入 JSON
将 pandas 导入为 PD


folder_path = “双语数据\史记\七十列传”


# 获取文件夹中的所有子文件夹，然后对于每个子文件夹，获取源文件和目标文件，
# 然后读取文件的内容，然后将它们组合成一个日期集，源文件是输入字段，
# 目标文件是 output 字段，目标文件是 output 字段

def get_files（folder_path）：
    子文件夹 = [f.f 在操作系统中的路径。scandir（folder_path） 如果 f.is_dir()]
    print（子文件夹)
    数据 = []
    
    source_file = “source.txt”
    target_file = “target.txt”
    对于子文件夹中的 x：
        其中 open（os.路径。join（x，source_file） ， “r”， encoding=“utf-8”） 作为 f：
            source_content = f。 读()
        其中 open（os.路径。join（x，target_file）， “r”， encoding=“utf-8”） 作为 f：
            target_content = f。 读()

        # 源和目标需要按 “\n” 进行拆分
        source_content = source_content。split（“\n”)
        target_content = target_content。split（“\n”)

        # source 和 target 应该逐行保存到 dateset 中
        对于 i in range（len（source_content））：
            数据集。append（[source_content[i]， target_content[i]])
        
    返回数据集

数据集 = get_files（folder_path)

# 在数据集中添加一列 “instruction”，内容为“请把古文翻译成现代汉语”
df = pd.DataFrame（dataset， columns=[“源”， “目标”])
df[“instruction”] = “请把现代汉语翻译成古文”

# 重命名列：source -> output、target -> input
df 的 intent 值。rename（columns={“source”： “输出”， “target”： “input”}， inplace=True)

# 打印数据集的长度
print（len（df))

# 将数据集保存到 jsonl 文件中
df 的 False。to_json（“dataset.jsonl”， orient=“records”， lines=True， force_ascii=False)
</script>
