FROM openjdk:8-jdk-alpine AS javajarcreator
RUN mkdir /home/app; cd /home/app; wget https://raw.githubusercontent.com/gopaljhunjhunwala/SampleServerApp/master/src/github/gopal/SampleServerApp.java; mkdir -p src/github/gopal/ ; mkdir classes; mv SampleServerApp.java ./src/github/gopal/;javac -d classes src/github/gopal/SampleServerApp.java; cd classes; echo Main-Class: github.gopal.SampleServerApp >manifest.txt; jar cvfm SampleServerApp.jar manifest.txt github/gopal/SampleServerApp.class; mv SampleServerApp.jar ../ ; cd .. ; rm -rf ./src ; rm -rf ./classes;
RUN ls /home/app
RUN echo image build successfully

FROM openjdk:8-jre-alpine
COPY --from=javajarcreator /home/app/SampleServerApp.jar /home/app/SampleServerApp.jar
EXPOSE 8088
ENTRYPOINT java -jar /home/app/SampleServerApp.jar