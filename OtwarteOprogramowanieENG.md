# How can you help with open source development?

Probably almost everyone has ever used open source software and many people use Gimp, Krita, Firefox, Blender or even Linux on a daily basis.

Due to the availability of source code and the possibility to modify it and use it for free even for commercial purposes, a community has developed around open source software that helps to translate texts or repair and create new code.

You too can join this community by helping to develop programs that you like and use.

## Translation
If we don't know too much about programming and/or we don't like to use a program that texts are not translated into our language (or other that we know), we can help you to change this by translating the interface or documentation.

The translations are usually can found on external services, e.g. Weblate, where you can start the translation process immediately after registration.

![Weblate](https://user-images.githubusercontent.com/41945903/81387047-53d50980-9116-11ea-845d-8f1e10588d0e.png)

Sample pages with translations:  
- Godot Engine - https://hosted.weblate.org/projects/godot-engine/godot/
- LibreOffice - https://translations.documentfoundation.org/
- Gnome - https://l10n.gnome.org/teams

Requirements:
- Good knowledge of at least two languages, including English
- A sense of good "taste" in translation

## Reporting bugs
This is the one of most basic way to support an open source project.

When reporting, it is important to provide as much information as possible about the system, version of the application and the situation in which the bug occurs, etc. because from my experience I can say that the more details are included in the report, the sooner this is fixed.

It is also important to name bug reports correctly, because very often bug reports are called "Please help me!!!" which result in the immediate closure of the thread and are often ignored by most users, and the "After clicking at Help button two windows opens instead of one" contains enough information for people who can help to get interested in the topic.

It is useful to include images, gifs, videos or even possible solutions to fix the problem.

When reporting bugs, please follow the previously prepared templates (if they exist, of course), but in special cases we can modify them a little if necessary.

Please note that we should create bug reports in English so that everyone can understand it (we can use the free [Deepl](https://www.deepl.com/translator)).

Sample template from the Godot Engine:
```
**Godot version.

**Oh, yes, yes, yes, yes, yes, yes, yes, yes.

**Issue description:**

**Steps to reproduce.

**Minimal reproduction project.
```
Example of a very good bug report  
[Useful](https://user-images.githubusercontent.com/41945903/81387004-428bfd00-9116-11ea-9a13-8b0014877307.png)

Requirements:
- Ability to describe the problem in a concise and in point

## Creating code 
This is probably one the most difficult ways to help open source projects, but at the same time none of them could develop without it.  

It is usually divided into two types:
- Create/remove functions
- Repairing existing errors

Creating or deleting pieces of source code is usually more difficult out of these two because it requires very good knowledge of the code and the style in which it is written in order to comply with it.

Fixing bugs very often requires a big knowledge and understanding of the code in order to find the part that does not work properly.  
However, sometimes a fast analysis of the code is enough.

Many errors are caused by common typos or incorrect use of tools/operators of a given language.
This kind of errors can be quite easily found with tools like Cppcheck, Address and Leak Sanitizer or Sonarcloud, which automatically scan the project for the incorrect code and display a list of errors in their opinion, which must be reviewed to see if they are wrong.

![Gimp](https://user-images.githubusercontent.com/41945903/81387115-7404c880-9116-11ea-9bf4-13ebcce2aae0.png)

Usually, creating or modifying the source code involves into several repetitive actions
- Getting know about the rules of code creation/bug fixing of given project  
https://github.com/godotengine/godot/blob/master/CONTRIBUTING.md

- Cloning the repository  
We have to clone our own repository and add a reference to the base one.
```
git clone https://github.com/username/godot.git
cd godot
git remote add upstream https://github.com/godotengine/godot.git
```
- Installing dependencies (programs required for application compilation)  
On Ubuntu this can usually be done with three commands (however, official documentation is recommended)
```
sudo sed -Ei 's/^# deb-src /deb-src /' /etc/apt/sources.list
sudo apt update

sudo apt build-dep -y godot
```
On other systems we have to find the instructions provided by the developers  
https://docs.godotengine.org/en/latest/development/compiling/

- Test compilation  
We should test the program to recompile it so we can be sure that the errors that may occur later are only the fault of our changes.
```
scons p=linuxbsd -j8
```
- Fixing an errors/adding code  
We are creating a new branch in the Git where we will change the code
```
git checkout -b "opengl_fix"
```
Then we add a specific functionality or fix to a specific bug using IDE or text editors such as VSCodium, QT Creator or vim.

- Compilation and checking  
After adding/changing the code we have to recompile app to check if everything works as it should.  
If there are any problems, we have to fix our code and try again.

- Adding files to the queue  
You should check which files have been changed and add the ones you want to include in our patch.
```
awesome
git add file1 folder2
```

- Creating and sending a commitment  
Once the patch is completed we can create a commit that can be included in the repository.  
We must keep in mind that we need to give it a good short title.
```
git commit -m "Fixes problem with OpenGL driver on AMD cards"
git push --set-upstream origin opengl_fix
```
- Creation of PR  
Now, through a web interface, we have to create a PR with our changes in Gitlab, Github or any other service, with an explanation inside what we exactly done.

![Console](https://user-images.githubusercontent.com/41945903/81387226-a4e4fd80-9116-11ea-8214-88d9fdfc1cee.png)

Requirements:
- Experience in writing code in the programming language used in the project
- Knowledge of the GIT version control system
- The ability to adapt the style of writing code to that used in the repository
- Knowledge of the basic commands in the console

## Using
While this may seem strange, even when using open-source software we can help.

We create habits, learn about the program's interface, get used to it, so there is a better chance that over time we will want to help in its development in other ways and that we will choose it instead of a commercial program.

![One](https://user-images.githubusercontent.com/41945903/81387318-c47c2600-9116-11ea-9f87-01b5420dbe90.png)

Requirements:
- Ymmmmmm... Well, using the program

## Promoting 
Advertising is very important in the world and one of the most effective forms is to recommend a product/program to friends or colleagues.

Therefore, if you like to use an open source program, it is a very good idea to recommend it to others if they need it.

It is important that in case of some simple problems, these people could ask you for help in solving them.

Requirements:
- Use of the program
- Basic knowledge about it and ability to use it

## Creating documentation 
Often in case of some problems with the program or looking for specific information about it we refer to its documentation.

Unfortunately, it happens that the documentation is missing or written in a difficult language that is hard to understand, so people have to waste time finding basic information on their own.

Therefore, for many projects, one of the main goals should be to create documentation that is friendly for both beginners and advanced users, so that most of the answers to the most frequently asked questions are included in it.

It is very important that the documentation does not contain many book definitions, but also has many examples from life.


![Docs](https://user-images.githubusercontent.com/41945903/81388155-26895b00-9118-11ea-96bc-1c9059d253b7.png)

Requirements: 
- Knowledge of the program
- Ability to convey information in a concise and simple manner

## Articles and Guides 
It often happens that the documentation is incomplete and does not answer frequent questions or is written in too difficult language.

In this case, therefore, if we have knowledge of a particular feature of the program, and for various reasons are unable to help with the documentation, then it is a good idea to create your own guide in which you have complete freedom in both subject and writing style.

![Krita](https://user-images.githubusercontent.com/41945903/81388300-68b29c80-9118-11ea-909d-8116c135c7d1.png)

Requirements:
- Knowledge of specific issues in program operation/configuration
- Writing skills

## Subsidies 
Although free software is usually distributed for free, this does not mean that people working on its development do not get paid for it.

Projects like Linux kernel are financed by huge companies paying programmers to work on it, but there are smaller projects like Linux Mint, Krita or Godot Engine that are developed largely from grants from ordinary people whose money is spent on developing and improving the program code and maintaining the physical infrastructure (servers, links etc.).

Typically, information about possible forms of support can be found on the project home page or in the repository.

![Dotacja](https://user-images.githubusercontent.com/41945903/81388444-94ce1d80-9118-11ea-9133-1430627b0e62.png)

Requirements:
- You must have free funds in your account ¯\\_(ツ)\_/¯

## Project management
As soon as we create our own repository, we automatically become its managers.

It is up to us to decide in what direction we will lead its development, what goals and principles we will set in it, or finally, what commits we will include in the project and what we will reject.

While it is quite simple to create a project in which you will manage it, becoming a decision-maker in another project usually requires involvement in the process of creating and verifying patches or discussing future changes in rules or new features.

You should also be able to say NO to ideas and changes that do not follow the project.

However, you should do so in a polite way, supporting it with a strong argumentation, because otherwise you can alienate with your unpleasant behaviour those who would like to help develop the project.

Requirements:
- Very good knowledge of the project code
- Experience in managing other projects (mainly required for larger projects)
- Calm and friendly - There's probably nothing worse than a rude person rejecting your PR in which you put a lot of work into

## Designing / Creating graphic elements
Although a huge amount of open source software is console versions (CLI), which is great for automating many activities, the GUI is also very often created, as many of the daily activities are easier to do and much more user-friendly.

In such applications, the look, readability and intuitiveness of the interface are crucial.

People with spatial planning skills can find themselves in planning where and what elements are to be found so that the user has no problems in finding and using a given thing.

It is also important that the icons in the design clearly and legibly indicate what they are for.

![Icons](https://user-images.githubusercontent.com/41945903/81536917-a4de3b00-936c-11ea-8378-c0946f00c8a0.png)

Requirements:
- Soul of the artist

## Summary
Open Source software is a common good used by crowds of people all over the world, which gives us the freedom to view, use and modify the source code of the application.

Although it's doubtful that we can use this code directly ourselves, there are people who, for us (and sometimes with our help, I sincerely encourage you to do so), will test, repair, and deliver the application to us, both for our convenience and for our privacy and security, which can be compromised by using software to which only a handful of people have access.


