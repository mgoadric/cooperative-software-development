There are numerous ways a software project can fail: projects can be over budget, they can ship late, they can fail to be useful, or they can simply not be useful enough. Evidence clearly shows that success is highly contextual and stakeholder-dependent: success might be financial, social, physical and even emotional, suggesting that software engineering success is a multifaceted variable that cannot be explained simply by user satisfaction, profitability or meeting requirements, budgets and schedules<ralph14>.

One of the central reasons for this is that there are many distinct *software qualities* that software can have and depending on the stakeholders, each of these qualities might have more or less importance. For example, a safety critical system such as flight automation software should be reliable and defect-free, but it's okay if it's not particularly learnable--that's what training is for. A video game, however, should probably be fun and learnable, but it's fine if it ships with a few defects, as long as they don't interfere with fun<murphy14>

There are a surprisingly large number of software qualities<boehm76>. Many concern properties that are intrisinc to a software's implementation:

* *Correctness* is the extent to which a program behaves according to its specification. If specifications are ambiguous, correctness is ambiguous. However, even if a specification is perfectly unambiguous, it might still fail to meet other qualities (e.g., a web site may be built as intended, but still be slow, unusable, and useless.)

* *Reliability* is the extent to which a program behaves the same way over time in the same operating environment. For example, if your online banking app works most of the time, but crashes sometimes, it's not particularly reliable.

* *Robustness* is the extent to which a program can recover from errors or unexpected input. For example, a login form that crashes if an email is formatted improperly isn't very robust. A login form that handles _any_ text input is optimally robust. One can make a system more robust by breadth of errors and inputs it can handle in a reasonable way.

* *Performance* is the extent to which a program uses computing resources economically. Synonymous with "fast" and "zippy". Performance is directly determined by how many instructions a program has to execute to accomplish it's operations, but it is difficult to measure because operations, inputs, and the operating environment can vary widely.

* *Portability* is the extent to which an implementation can run on different platforms without being modified. For example, "universal" applications in the Apple ecosystem that can run on iPhones, iPads, and Mac OS without being modified or recompiled are highly portable.

* *Interoperability* is the extent to which a system can seamlessly interact with other systems, typically through the use of standards. For example, some software systems use entirely proprietary and secret data formats and communication protocols. These are less interoperable than systems that use industry-wide standards.

* *Security* is the extent to which only authorized individuals can access a software system's data and computation.

Whereas the above qualities are concerned with how software behaves technically according to specifications, some qualities concern properties of how developers interact with code:

* *Verifiability* is the effort required to verify that software does what it is intended to do. For example, it is hard to verify a safety critical system without either proving it correct or testing it in a safety-critical context (which isn't safe). Take driverless cars, for example: for Google to test their software, they've had to set up thousands of paid drivers to monitor and report problems on the road. In contrast, verifying that a simple static HTML web page works correctly is as simple as opening it in a browser.

* *Maintainability* is the effort required to correct, adapt, or perfect software. This depends mostly on how comprehensible and modular an implementation is.

* *Reusability* is the effort required to use a program's components for purposes other than those for which it was originally designed. APIs are reusable by definition, whereas black box embedded software (like the software built into a car's traction systems) is not.

Other qualities are concerned with the use of the software in the world by people:

* *Learnability* is the ease with which a person can learn to operate software. Learnability is multi-dimensional and can be difficult to measure, including aspects of usability, expectations of prior knowledge, reliance on conventions, error proneness, and task alignment<grossman09>.

* *User efficiency* is the speed with which a person can perform tasks with a program. For example, think about the speed with which you can navigate back to the table of contents of this book. Obviously, because most software supports many tasks, user efficiency isn't a single property of software, but one that varies depending on the task.

* *Accessibility* is the extent to which people with varying cognitive and motor abilities can operate the software as intended. For example, software that can only be used with a mouse is less accessible than something that can be used with a mouse, keyboard, or speech recognition. Software can be designed for all abilities, and even automatically adapted for individual abilities<wobbrock11>.

* *Privacy* is the extent to which a system prevents access to information that intended for a particular audience or use. To achieve privacy, a system must be secure; for example, if anyone could log into your Facebook account, it would be insecure, and thus have poor privacy preservation. However, a secure system is not necessarily private: Facebook works hard on security, but shares immense amounts of private data with third parties, often without informed consent.

* *Consistency* is the extent to which related functionality in a system leverages the same skills, rather than requiring new skills to learn how to use. For example, in Mac OS, quitting any application requires the same action: command-Q or the Quit menu item in the application menu; this is highly consistent. Other platforms that are less consistent allow applications to have many different ways of quitting applications.

* *Usability* is an aggregate quality that encompasses all of the qualities above. It is used holistically to refer to all of of those factors. Because it is not very precise, it is mostly useful in casual conversation about software, but not as useful in technical conversations about software quality.

* *Bias* is the extent to which software discriminates or excludes on the basis of some aspect of its user, either directly, or by amplifying or reinforcing discriminatory or exclusionary structures in society. For example, data used to train a classifier might used racially biased data, algorithms might use sexist assumptions about gender, web forms might systematically exclude non-Western names and language, and applications might be only accessible to people who can see or use a mouse. Inaccessibility is a form of bias.

* *Usefulness* is the extent to which software is of value to its various stakeholders. Utility is often the _most_ important quality because it subsumes all of the other lower-level qualities software can have (e.g., part of what makes a messaging app useful is that it's performant, user efficient, and reliable). That also makes it less useful as a concept, because it encompasses so many things. That said, usefulness is not always the most important quality. For example, if you can sell a product to a customer and get a one time payment of their money, it might not matter--at least to a for-profit venture--that the product has low usefulness.

Although the lists above are not complete, you might have already noticed some tradeoffs between different qualities. A secure system is necessarily going to be less learnable, because there will be more to learn to operate it. A robust system will likely be less maintainable because it it will likely have more code to account for its diverse operating environments. Because one cannot achieve all software qualities, and achieving each quality takes significant time, it is necessary to prioritize qualities for each project.

These external notions of quality are not the only qualities that matter. For example, developers often view projects as successful if they offer intrinsically rewarding work<procaccino05>. That may sound selfish, but if developers _aren't_ enjoying their work, they're probably not going to achieve any of the qualities very well. Moreover, there are many organizational factors that can inhibit developers' ability to obtain these rewards. Project complexity, internal and external dependencies that are out of a developers control, process barriers, budget limitations, deadlines, poor HR planning, and pressure to ship can all interfere with project success<lavallee15>.

As I've noted before, the person most responsible for isolating developers from these organizational problems, and most responsible for prioritizing software qualities is a product manager. Check out the podcast below for one product manager's perspectives on the challenges of balancing these different priorities.