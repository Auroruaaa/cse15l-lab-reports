# CSE 15L Lab Report 4

Beijie Cheng | Nov. 4, 2023

----------

1、Log into ieng6 (Step 4)

<img width="514" alt="Screenshot 2023-11-15 at 17 37 05" src="https://github.com/Auroruaaa/cse15l-lab-reports/assets/116754028/4fdbe739-3d25-49e1-b007-4c2994de0124">

> `<up> <enter>`

> I pressed `up arrow` to get to the ssh command in my history, and then pressed `enter` to run the command. Since it does not need my password, it directly connected to the Server ieng6.

2、Clone your fork of the repository from your Github account using the SSH URL(Step 5)

<img width="559" alt="Screenshot 2023-11-15 at 17 45 12" src="https://github.com/Auroruaaa/cse15l-lab-reports/assets/116754028/dd61077b-7d2d-4dc0-a34f-9a2eeea47bf4">

> `<ctrl c>` `git clone <ctrl v> <enter>`

> I first copy the SSH URL for github by using `ctrl c`. Then in the terminal, I typed `git clone` and then paste the SSH URL using `ctrl v`, and pressed `enter` to clone the folder 'lab7'.
> I also used the command `ls` and then `enter` to check if the folder 'lan7' was cloned correctly.

3、Run the tests, demonstrating that they fail (Step 6)

<img width="559" alt="Screenshot 2023-11-15 at 21 34 51" src="https://github.com/Auroruaaa/cse15l-lab-reports/assets/116754028/b9f5f0fc-a27e-4e49-95fe-b4c0759fb7f8">

> `cd lab7 <enter>` `<ctrl r> bash <enter>`

> In this section, I first used `cd lab7` to enter the directory that I want to work with. Then I used `ctrl r` to search for my history in the terminal, and typed `bash` to find my previous commands. Then I pressed `enter` to compile the test.sh and run the tests.

4、Edit the code file to fix the failing test (Step 7)

<img width="562" alt="Screenshot 2023-11-15 at 21 37 58" src="https://github.com/Auroruaaa/cse15l-lab-reports/assets/116754028/f408fd5d-5cd4-4f2e-a18b-8420cbe00155">

> `vim ListExamples.java <enter>` `/index1 n n e x i 2 <esc> :wq`

> To edit the file, I used `vim ListExamples.java` to open the file in the terminal. Then, I used the command `/index1` and `n` (next line) to locate my cursor to the line I want to edit. After I reached the line, I pressed `e` to get to the last character of 'index1', and pressed `x` to delete the character '1'. Then, I pressed `i` to enter the insert mode and typed the correst character '2'. After I finish changing the error, I pressed `esc` to switch back to Normal Mode. Finally, I used `:wq` to save and exit the file.

5、Run the tests, demonstrating that they now succeed (Step 8)

<img width="479" alt="Screenshot 2023-11-15 at 21 44 33" src="https://github.com/Auroruaaa/cse15l-lab-reports/assets/116754028/9d1ed1f5-df46-4800-8877-daadad3c8b1d">

> `<up> <enter>`

> I used up arrow twice for my bash history of the command `bash test.sh` to run the tests again. This time all the tests are passed.

6、Commit and push the resulting change to your Github account (Step 9)

<img width="500" alt="Screenshot 2023-11-15 at 21 47 26" src="https://github.com/Auroruaaa/cse15l-lab-reports/assets/116754028/d6c0353b-dfd4-46ad-8aff-31fbc16a3409">

> `git add ListExamples.java <enter>` `git commit <enter>` `G i Change for labrepo <esc> :wq` `git push <enter>`

> Firstly, I used `git add ListExamples.java` to add the file I want to commit. Then I compile the command `git cimmit` and the terminal will show the window for me to update the comments for committing the file. I pressed capital `G` to get to the end of the contents, and pressed `i` to switch into insert mode. Then I added the comment `Changes for labrepo` to the file and pressed `esc` to switch back to Normal Mode. To save and exit, I typed `:wq` to get back to the termial, and it shows my changes for the git commit. Lastly, I used the command `git push` to push my changes to the github webpage.




