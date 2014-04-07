
This is Beverly's Spring MVC email tutorial
================================

This tutorial is for people who know some Java, but who don't know really anything about Spring MVC.  I had to learn how to send an email from a web app, and my learning coach helped me figure this out.  I thought I'd pass it on to you.

This tutorial will take you through:

- Hello World!
- Hello Email!
- Creating Spring MVC "beans"
- Hooking up Spring MVC beans with your code
- Sending an email with code!


Some housekeeping
-----------------

I hate programming tutorials that use function and instance names that look
like offical names.  There are so many function names and instances in
tutorials that are totally user-defined.  Basically::

    Name it whatever-you-want, and it will still work!

Instead of using willy-nilly names like "lulu", I will append "_lulu" to
the end of logical names, so it will be entirely obvious which names can be
changed with no penalty.  And, it will give you an idea of what "real"
programmers might use to call a certain function (hint: just drop the "_lulu").
Naming things well is certainly a skill to be desired.


Create a hello world Java app
-----------------------------

I know you probably have already made one of these before, but let's do this together!  Create a file called Main.java, and make it look like this::

    public class Main {
        public static void main(String[] args) {
            System.out.println("Hello world");
        }
    }

With just this, you should be able to compile and run (and greet the world!).  I compile and run through Intelli-J, but

    >> javac Main.java
    >> java Main

Next, create an EmailSender class; call it EmailSender.java, and make it look like this::

    public class EmailSender {
        public void sendMail() {
            System.out.println("Hello email!");
        }
    }

And then make sure you call it from Main.  Here's an updated view of Main.java::

    
    public class Main {
        public static void main(String[] args) {
            System.out.println("Hello world");
	    EmailSender emailSender = new EmailSender();
	    emailSender.sendMail();
        }
    }

Compile and run again (javac, java).  And see it print out::

Hello world
Hello email!

In the next section, we'll create a Spring MVC bean.  I'll try to explain what it is, too.