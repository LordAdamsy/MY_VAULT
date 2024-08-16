1. 项目目录下新建conponent目录
2. conponent目录中新建需要的组件目录
3. 组件目录中包含.c和.h文件，以及CMakeLists.txt文件
4. .h需要条件编译
5. component下的CMakeLists.txt文件如需要driver中的库，则要添加REQUIRES driver
6. 在项目目录下的CMakeLists.txt文件中添加编译路径：
		set(EXTRA_COMPONENT_DIRS "${EXTRA_COMPONENT_DIRS} $PATH")
		$PATH:组件目录的路径