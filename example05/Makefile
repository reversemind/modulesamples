#
# Example5 for the Java 9 talk
#
# (c)2016, Ivan Krylov
#
#

JAVA_HOME=/Users/ivan/openjdk9_build/images/jdk-bundle/jdk-9.jdk/Contents/Home
PATH=${JAVA_HOME}/bin

JAR=${JAVA_HOME}/bin/jar
JAVA=${JAVA_HOME}/bin/java
JAVAC=${JAVA_HOME}/bin/javac
JMOD=${JAVA_HOME}/bin/jmod
JLINK=${JAVA_HOME}/bin/jlink
MODDIR=${JAVA_HOME}/jmods

all: show

compile: module1 module2 moduleMain

module1:
	@echo == What is in com.azul.modules.module1 ==
	@tree com.azul.modules.module1
	@echo == Let\'s compile ==
	${JAVAC} --module-source-path .  -d target com.azul.modules.module1/module-info.java
	${JAVAC} --module-source-path .  -d target com.azul.modules.module1/com/azul/testpackage/A.java

module2:
	@echo == What is in com.azul.modules.module2 ==
	@tree com.azul.modules.module2
	@echo == Let\'s compile ==
	${JAVAC} --module-source-path .  -d target com.azul.modules.module2/module-info.java
	${JAVAC} --module-source-path .  -d target com.azul.modules.module2/com/azul/testpackage/A.java

moduleMain: module1 module2
	@echo == What is in com.azul.modules.moduleMain ==
	@tree com.azul.modules.moduleMain
	echo ${JAVAC}
	@echo == Let\'s compile ==
	${JAVAC} -p ${MODDIR}:/Users/ivan/mygithub/modulesamples/example05/target -d target/com.azul.modules.moduleMain com.azul.modules.moduleMain/module-info.java
	${JAVAC} -p ${MODDIR}:/Users/ivan/mygithub/modulesamples/example05/target -d target/com.azul.modules.moduleMain com.azul.modules.moduleMain/com/azul/runpackage/Example05.java

module1jar: module1
	mkdir -p mlib
	${JAR} --create --file=mlib/module1.jar -C target/com.azul.modules.module1 .

module2jar: module2
	mkdir -p mlib
	${JAR} --create --file=mlib/module2.jar -C target/com.azul.modules.module2 .

moduleMainjar: module1jar module2jar moduleMain
	mkdir -p mlib
	${JAR} --create --file=mlib/moduleMain.jar --main-class=com.azul.runpackage.Example05 -C target/com.azul.modules.moduleMain .

run: compile
	${JAVA} -p target -m com.azul.modules.module2/com.azul.testpackage2.A

jarshow: compile module1jar module2jar moduleMainjar
	@echo == What is in mlib ==
	@tree mlib
	@echo == Time to Run jars! ==
	${JAVA} -p mlib -m com.azul.modules.moduleMain

clean:
	rm -rf mlib target image jmod onlyExample
