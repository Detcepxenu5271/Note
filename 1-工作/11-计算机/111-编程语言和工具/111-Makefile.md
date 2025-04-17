# Makefile


## 快速使用
Makefile 由一系列规则构成，规则的结构为：
> 目标文件：依赖文件
> 	命令 1
> 	命令 2
> 	...
> 	命令 n

注意：命令必须以 Tab 开头（不能用空格）

默认目标：一定是第一个目标（不管是文件还是伪目标）

伪目标
* 使用`.PHONY`指定的作用：即使存在同名文件，这个也是伪目标

## 模板
### C
[C、C++的Makefile模板 - Raina_R - 博客园 (cnblogs.com)](https://www.cnblogs.com/raina/archive/2019/09/27/11599074.html)

```Makefile
# notdir: 从包含目录的文件名序列中取文件名 (如 src/a.c -> a.c)
# CURDIR: Current Dir
TARGET = ${notdir $(CURDIR)} 

SRC_DIR = .
SRC_SUBDIR += . 
INCLUDE_DIR += .
OBJ_DIR = .

CC = gcc
C_FLAGS = -g -Wall
# LD: 链接, Loader
LD = $(CC)
INCLUDES += -I$(INCLUDE_DIR)
LD_FLAFS += 
LD_LIBS =

ifeq ($(CC), g++)
	TYPE = cpp
else
	TYPE = c
endif

SRCS += ${foreach subdir, $(SRC_SUBDIR), ${wildcard $(SRC_DIR)/$(subdir)/*.$(TYPE)}}
# patsubst: $(patsubst <pattern>,<replacement>,<text>), 如果 <text> 符合 <pattern>, 则替换为 <replacement>
OBJS += ${foreach src, $(notdir $(SRCS)), ${patsubst %.$(TYPE), $(OBJ_DIR)/%.o, $(src)}}

# vpath <pattern> <directories>: 为符合 <pattern> 模式的文件指定搜索目录 <directories>
# 在 $(OBJS) 的生成规则用到了
vpath %.$(TYPE) $(sort $(dir $(SRCS)))

all : $(TARGET)
	@echo "Builded target:" $^
	@echo "Done"

$(TARGET) : $(OBJS)
# mkdir -p: 允许创建嵌套目录 (如 a/b/c)
# $(@D): $@ 的目录部分 ($(@F) 就是文件部分)
	@mkdir -p $(@D)
# TODO test
	@echo "test: prerequisites dir part:" $(^D)
	@echo "Linking" $@ "from" $^ "..."
	$(LD) -o $@ $^ $(LD_FLAGS) $(LD_LIBS)
	@echo "Link finished\n"

# static pattern rule:
# $(OBJS) 是一系列目标文件, 需要在依赖部分用 pattern 匹配, 确定依赖规则
# 这里表示形如 $(OBJ_DIR)/%.o 的文件应该依赖 %.$(TYPE) 文件
# 实际执行时, 对 $(OBJS) 中的每个文件, 都会执行一次下列命令
$(OBJS) : $(OBJ_DIR)/%.o:%.$(TYPE)
	@mkdir -p $(@D)
	@echo "Compiling" $@ "from" $< "..."
	$(CC) -c -o $@ $< $(C_FLAGS) $(INCLUDES)
	@echo "Compile finished\n"

.PHONY : run clean cleanobj
run : all
	./$(TARGET)
clean : cleanobj
	@echo "Remove all executable files"
	rm -f $(TARGET)
cleanobj :
	@echo "Remove object files"
	rm -rf $(OBJ_DIR)/*.o
```

## 参考资料

[GNU Make 教程（英文）](https://www.gnu.org/software/make/manual/make.html)

这个教程好：[跟我一起写 Makefile](https://seisman.github.io/how-to-write-makefile/introduction.html)
