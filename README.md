# Seq2Seq_TensorFlow_QA
基于Seq2Seq与TensorFlow的中文QA robot

训练

下面的参数仅仅为了测试，训练次数不多，不会训练出一个好的模型

size: 每层LSTM神经元数量

num_layers: 层数

num_epoch: 训练多少轮（回合）

num_per_epoch: 每轮（回合）训练多少样本

具体参数含义可以参考train.py

运行：

```
python3 s2s.py --size 512 --num_layers 2 --num_epoch 5 --batch_size 64 --num_per_epoch 100000 --model_dir ./model/model1
```

其中：如果需要更好的效果，可以将size和num_per_epoch分别增加到1024和500000
```

输出：在 model/model1 目录会输出模型文件，上面的参数大概会生成700MB的模型

如果是GPU训练，尤其用的是<=4GB显存的显卡，很可能OOM(Out Of Memory)，
这个时候就只能调小size，num_layers和batch_size

## 测试

下面的测试参数应该和上面的训练参数一样，只是最后加了--test true 进入测试模式


```
运行：

```
python3 s2s.py --size 512 --num_layers 2 --num_epoch 5 --batch_size 64 --num_per_epoch 100000 --model_dir ./model/model1 --test true


```

输出：在命令行输入问题，机器人就会回答哦！但是上面这个模型会回答的不是很好……当然可能怎么训练都不是很好，不要太期待～～




---------------------------------如果你想训练自己的模型---------------------------------------

## 第一步

输入：首先从[这里](https://github.com/rustch3n/dgk_lost_conv)下载一份dgk_shooter_min.conv.zip

输出：然后解压出来dgk_shooter_min.conv文件

我用的是小黄鸡的语料库

## 第二步

在***项目录下***执行decode_conv.py脚本

输入：python3 decode_conv.py

输出：会生成一个sqlite3格式的数据库文件在db/conversation.db

## 第三步

在***项目录下***执行data_utils.py脚本

输入：python3 data_utils.py

输出：会生成一个bucket_dbs目录，里面包含了多个sqlite3格式的数据库，这是将数据按照大小分到不同的buckets里面

例如问题ask的长度小于等于5，并且，输出答案answer长度小于15，就会被放到bucket_5_15_db里面

