# HTB Academy Structure

In HTB Academy, we break the material into digestible chunks to enable a seamless understanding of the content. The largest learning block is a `path`, which is broken into multiple `modules`, each of which covers a specific self-contained topic. Modules are further broken down into multiple `sections`.

Some paths are linked to certifications, which can be obtained after completing their path and `exam`.

![alt](https://academy.hackthebox.com/storage/modules/15/structure2.png)

While a major step, like a path, `may look intimidating` and heavy with information, breaking it into modules and sections `makes it much more digestible and easier to learn`. This allows anyone to start with a single section, and take small steps until they reach their major achievement by obtaining a certificate.

![alt](https://academy.hackthebox.com/storage/modules/15/small_steps.png)

This process not only allows you to `take it one step at a time`, but also ensures that you are `constantly testing your knowledge and challenging your skills`, which is necessary to reaffirm the knowledge gained through modules and turn it into gained skills.

_“Great things are not done by impulse, but by a series of small things brought together.”_ **Vincent Van Gogh**


# Modules

## What is a Module?

A `module` is the core building block within HTB Academy, and represents a single course that covers a specific topic. Modules consist of multiple `sections`, as mentioned previously, and a group of modules makes a `path`.

You can click on any module in the [Modules](https://academy.hackthebox.com/modules) page to preview its summary, which mentions what the module covers, what is the expected outcome, and what are the requirements for starting the module (if any).

**Note:** You can click on the () icon to add a module to your favorite "i.e. `To-Do`" list, which can be accessed from the [Dashboard](https://academy.hackthebox.com/dashboard).

## Types of Modules

HTB Academy modules are categorized into: `Offensive`, `Defensive`, and `General` modules. They are also rated based on their difficulty, as: `Fundamental`, `Easy`, `Medium`, and `Hard`.

You can filter modules based on the above categories (and other criteria) in the [Modules](https://academy.hackthebox.com/modules) page. Furthermore, you can filter modules by name to find the exact module you are looking for.

![](https://academy.hackthebox.com/storage/modules/15/new_bar.png)

## Module Tiers

Modules are split into `5 Tiers` based on their cost, as follows:

|Tier|Cost|Reward|
|---|---|---|
|Tier 0 (free)|10|10|
|Tier I|50|10|
|Tier II|100|20|
|Tier III|500|100|
|Tier IV|1000|200|

Each module costs a specific `amount of cubes` to unlock, and will always `return 20% of those cubes` back upon 100% completion of the module.

`Tier 0` modules are considered `free modules`, as they cost 10 cubes and reward back 10 cubes, thus not affecting your remaining cubes balance. Remember, `you must complete the module` to gain back the cubes, which is done to incentivize students to complete each module.

The `Tier` of a module does not reflect its `difficulty`.

**Note:** If you have an annual subscription, then included modules will cost you 0 cubes, while still giving you back their reward.

## Completing a Module

To complete a module, you need to solve all of its exercises and mark all sections as "completed". Once that's done, you will usually face the module's `Skills Assessment`, which represents a real-world scenario of the topic the module covered, and tests your understanding of most/all of the skills shown within it.

If you are able to complete the module's skills assessment, then you will have demonstrated that you have a solid understanding of the module's content, and can thus move to your next module. To do so, simply click on the `Finish` button found at the last section in the module (often the Skills Assessment section).

![](https://academy.hackthebox.com/storage/modules/15/finish_module.png)

When you finish a module, you will be redirected to its `Completion` page. Here, you can `share your achievement` on social media, `write a review for the module`, and find suggestions for modules to do next. You will also unlock the `module's badge`, which you can find on the [My Badges](https://academy.hackthebox.com/my-badges) page.

# Exercises

## What is an Exercise?

In addition to the examples and demos demonstrated within interactive sections, most also end with exercises to test that knowledge.

An exercise will usually have an accompanying `Docker target` or `VM target(s)`. A target can be started by clicking on `Click here to spawn the target system!`, which will be populated with its access details, in the format `http://<ip>:<port>`. It may also provide authentication details, in the form of a `username` and `password`.

![](https://academy.hackthebox.com/storage/modules/15/target_example.png)

**Note:** Only a single target per user can be active at any one time. Each target has a timer that shows how much time is left before it is terminated, but it can be manually extended or re-spawned by clicking on the appropriate buttons.

## Docker Targets

Most exercises, especially in web modules, utilize Docker targets, which are faster to spawn and can be accessed without any additional setup.

Once a docker target is active, you can simply click on the IP/PORT to copy it, and then access the target (e.g. in a web browser for web modules). Most docker targets are ready to use instantly, although some may take up to a minute after the IP/PORT are shown.

![alt text](https://academy.hackthebox.com/storage/modules/15/solving_interactive_exercise.gif)

**Note:** You can spot a docker target by its lack of a VPN button, as no VPN connection is required to access it.

## VM Targets

Certain modules have advanced requirements for their exercises, like a Windows target, an Active Directory (AD) target, or a network environment target. Such modules utilize a Virtual Machine (VM) as their target, which can be spawned like docker targets, but may take a little longer to start.

If you use your `Workstation`, then you can start accessing the VM once its IP is shown. Otherwise, if you prefer to use your own machine, then the VM can be accessed by connecting to the provided VPN key, which can be downloaded by clicking on the `Download VPN Connection File` button.

![alt text](https://academy.hackthebox.com/storage/modules/15/vm_example.jpg)

**Note:** To find out more about connecting to the HTB Academy VPN, check out [this help article](https://help.hackthebox.com/en/articles/9297532-connecting-to-academy-vpn).

## Completing an Exercise

Some questions have a `Hint` button, which may point you in the right direction if you are struggling with them. Once you obtain the answer or the flag, you can type it in the field and hit `Submit` to complete the exercise/question.

Solving a question correctly will reward you a certain amount of () cubes, which may be collected to unlock other modules in HTB Academy, as we will discuss in the next section.

Most questions are required to complete the section, but any questions marked as `Optional Exercises` may be solved by clicking the `Reveal Answer` button, and the section may be completed without solving them.

**Note:** You can always use the exercise targets to practice what was shown in the section. However, solving the exercise will not always match the exact commands shown in the section, as they will have some variance to test your understanding and gradually build your skills. Exercises in easier modules will have a minor variance from the shown demo, while harder modules will be more challenging.