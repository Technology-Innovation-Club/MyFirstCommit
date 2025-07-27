# MyFirstCommit
### Welcome to Technology Innovation Club!!
This repository is designed to help new members familiarize themselves with Git and GitHub by practicing common workflows such as forking, cloning, committing, and creating pull requests.

### 1. Fork the Repository
Forking creates a personal copy of this repository in your GitHub account.
- Click on the **"Fork"** button at the top right corner of the repository page.
- Your GitHub account will now have a copy of this repository.

### 2. Clone Your Fork
Now, download your forked repository to your computer.
- Click the **"Code"** button in your forked repository.
- Copy the HTTPS or SSH link.
- Open your terminal (Command Prompt, Git Bash, or VS Code terminal) and run:

  ```sh
  git clone https://github.com/YOUR-USERNAME/git-intro.git
  ```

  _(Replace `YOUR-USERNAME` with your actual GitHub username.)_

- Move into the cloned folder:

  ```sh
  cd git-intro
  ```

### 3. Add Your Name to `members.md`
- Open the repository folder in a text editor (VS Code, Sublime, etc.).
- Open the `members.md` file.
- Add your details in the format below:

  ```md
  - Name: Your Name
    Course: Your Course
    Year: What year it is
    Profession: Cybersecurity,Designer,Fullstack Developer,Product Manager
  ```

  **Example:**
  ```md
  - Name: John Doe
    Course: Computer Science
    Year: 2025
    Profession: Back-end Dev
  ```

### 4. Stage Your Changes
After adding your details, save the file and go back to the terminal. Run:

```sh
git add members.md
```

This stages your changes so Git can track them.

### 5. Commit Your Changes
Now, commit the changes with a descriptive message:

```sh
git commit -m "Added [Your Name] to members.md"
```

_(Replace `[Your Name]` with your actual name.)_

### 6. Push Changes to Your Forked Repo
Now, send the changes to your GitHub account:

```sh
git push origin main
```

_(If the repository uses `master` instead of `main`, use `git push origin master`.)_

### 7. Create a Pull Request (PR)
- Go to your forked repository on GitHub.
- Click on **"Compare & pull request"**.
- Add a message like:  
  **"Added [Your Name] to members.md"**
- Click **"Create pull request"**.

🎉 **You did it!** 🎉 Now, wait for your PR to be reviewed and merged.

---

## Need Help?
If you’re stuck, don’t worry! Here’s what you can do:
- Ask any of the club leads for help
- Ask for help in discussions 
- Check out GitHub’s [official documentation](https://docs.github.com/en/get-started).
- Watch Git tutorials on [YouTube](https://www.youtube.com/results?search_query=git+and+github+tutorial)
