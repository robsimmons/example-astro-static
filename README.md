# Example disco Astro static site

You can clone this repo, OR you can do the following six steps to make the repo yourself:

1. Create a site with Astro:

   ```sh
   npm create astro@latest
   ```

   This will walk you through creating an Astro site.

2. [Create a new repository on github](https://github.com/new). These instructions will refer to the repository as USERNAME/REPONAME, but it'll actually be something like `john/my-site`.

3. Navigate to the directory that you created:

   ```sh
   cd REPODIR
   ```

   above, replace `REPODIR` with whereever you told Astro to put your project (e.g. `./my-project`).

4. Push your new site to github:

   ```sh
   git remote add origin git@github.com:USERNAME/REPONAME.git
   git branch -M main
   git push -u origin main
   ```

   above, replace `USERNAME/REPONAME` with your username and the repository you created (e.g. `john/my-project`)

3. Add [this Dockerfile](Dockerfile) to your project:

   ```
   FROM node:latest

   WORKDIR /code

   # start with dependencies to enjoy caching
   COPY ./package.json /code/package.json
   COPY ./package-lock.json /code/package-lock.json
   RUN npm install

   # copy rest and build
   COPY . /code/.
   RUN --mount=type=secret,id=.env env $(cat /run/secrets/.env | xargs) npm run build
   ```

4. Add [this disco.json file](disco.json) to your project:

   ```
   {
       "version": "1.0",
       "services": {
           "web": {
               "type": "generator"
           }
       }
   }
   ```

5. Add those files to git and push:

   ```sh
   git add Dockerfile disco.json
   git commit -a -m "Ready to disco 🪩"
   git push
   ```
