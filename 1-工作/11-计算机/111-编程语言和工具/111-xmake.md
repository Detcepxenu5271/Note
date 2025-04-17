# xmake
[xmake tutorial](https://xmake.io/#/zh-cn/about/introduction)
[A Tour of xmake](https://www.zhihu.com/column/c_1537535487199281152)

## 杂项
基本使用: xmake 命令, 自动生成 xmake.lua

指定工具链: `xmake f --toolchain=xxx`, 也可以在 xmake.lua 中设置 `set_toolchains("xxx")`

### 参考xmake编写格式 (来源: 本科毕设)
```
-- 用于参考的 xmake.lua

-- 使用MLIR的项目编译, C++库
set_languages("c++17")

target("toyc-ch1")
	set_kind("binary")
	set_targetdir("bin")
	add_includedirs("include")
	add_linkdirs("/usr/local/lib")
	add_links("MLIRSupport", "LLVMSupport", "LLVMDemangle", "rt", "dl", "m", "z", "tinfo", "xml2")
	add_files("toyc.cpp", "parser/AST.cpp")
	add_cxxflags("-fno-rtti")
	set_toolchains("clang")

--snnl项目, 自定义命令
set_languages("c++17")


target("antlr")
	set_kind("phony")
	-- add_files("grammar/*.g4")

	on_build(function (target)
		-- antlr 好像会在生成的文件前加上 g4 文件的路径
		os.cd('grammar')
		os.run("antlr-cpp -no-listener -visitor -o ../gen/antlr *.g4")
		os.cd('..')
		-- 可以用 os.runv, 参数以列表传递, 可设置环境变量
		-- exec/execv 和 run 的区别在于, exec 有标准输出, run 只有错误输出
		-- os.execv("antlr-cpp", {"grammar/*.g4", "-no-listener", "-o generated/"}, {stdout = xxx, stderr = xxx, envs = xxx})
	end)

	on_clean(function (target)
		os.rm("gen/antlr/*.h")
		os.rm("gen/antlr/*.cpp")
		os.rm("gen/antlr/*.tokens")
		os.rm("gen/antlr/*.interp")
	end)


target("ast")
	set_kind("binary")
	set_targetdir("bin")
	set_toolchains("clang")

	add_deps("antlr")

	add_files("src/*.cpp")
	add_files("gen/antlr/*.cpp")
	add_includedirs(
		"include",
		"gen/antlr",
		"/usr/local/include/antlr4-runtime"
	)
	add_linkdirs("/usr/local/lib")
	add_links("antlr4-runtime")
```