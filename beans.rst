Using Spring MVC beans
================================

What the hell is a Spring MVC bean, you ask?  Yes, I was also confused a lot before.  And, by "before", I mean like 12 hours ago.  Hopefully I can explain the things that helped me understand what Spring MVC beans are and what they do.

Here are some things that helped me understand stuff

- Seeing a single bean by itself
- Seeing a single bean by itself hold variables that correspond to a particular class
- Seeing the ID of the bean be equal to lulu-whatever
- Seeing the class of the bean be restricted to the class that it corresponds to
- Realizing that a bean is just an instance of a class, but written in a weird Spring MVC way
- Using the bean in a standalone Java context (using it in a website is out-of-scope for this tutorial)

So, everything's great!  I'll show you!

Making a configuration file
---------------------------

Nope, it's not called config.  It's called applicationContext.xml.  This is xml code, where all the Spring MVC "beans" are defined.  What is a bean?  It's... well, I'll just show you.

Create a file called applicationContext.xml, and make it look like this::

    <?xml version="1.0" encoding="UTF-8"?>
    <!DOCTYPE beans PUBLIC "-//SPRING//DTD BEAN//EN" "http://www.springframework.org/dtd/spring-beans.dtd">
    <beans>
        <bean id="lulu_EmailSender" class="EmailSender">
        </bean>
    </beans>

You can try compiling and running now, but nothing will have changed.  Let's make an instance parameter in EmailSender, so we can later hook it up to the bean.

Open EmailSender.java and edit it to look like this::

    public class EmailSender {
    
        private String lulu_name;
    
        public void sendMail() {
            System.out.println("Hello " + lulu_name + "!");
        }
    }

You can run this now, but it won't be pretty.  We haven't initialized name, so it'll just return null.  If you compile and run, you should see something like::

    Hello world
    Hello null!

Okay, so let's put a name in there!  Let's do it through applicationContext!  Open applicationContext.xml, and make it look like this::

    <?xml version="1.0" encoding="UTF-8"?>
    <!DOCTYPE beans PUBLIC "-//SPRING//DTD BEAN//EN" "http://www.springframework.org/dtd/spring-beans.dtd">
    <beans>
        <bean id="lulu_EmailSender" class="EmailSender">
            <property name="name" value="Lulu"/>
        </bean>
    </beans>

You should note that property name is equal to "name", which is the variable name in our EmailSender class.  The value is where we initialize the instance variable.  Here, our "name" is "Lulu".  (I just made up that name.  Put your own name there if you'd like.)

Name should be red colored, if you're using an IDE.  There's no setter for "name", and so the applicationConfiguration.xml file cannot set the instance variable equal to the value you gave.  Let's make a setter for name in EmailSender.java.  Open EmailSender.java, and make it look like this::

    public class EmailSender {

        private String lulu_name;

        public void sendMail() {
            System.out.println("Hello " + lulu_name + "!");
        }

        public void setName(String name) {
            this.name = name;
        }
    }

We're almost there.  (I'm sorry this isn't very interactive.  I think Spring MVC is just like that.)  There's one more step:  telling the Main class to access the bean.  Since we're not using Spring MVC in a web context, we're going to have to cast the bean to an EmailSender.  We do this using a function from Spring MVC (see this website:  http://alvinalexander.com/blog/post/java/load-spring-application-context-file-java-swing-application, which explains how to use beans in a standalone Java context).

