# 5e.tools

Visit the [main site](https://5e.tools/index.html) or go to the unofficial GitHub [mirror](index.html).

[Join the 5etools Discord here!](https://discord.gg/5etools)

## Help and Support

Please see [our wiki](https://wiki.tercept.net/) for FAQs, installation guides, supported integrations, and more.

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md).

## License

This project is licensed under the terms of the MIT license.

> Lean Fork Note: Removed pages/utilities: Initiative Tracker Player View, RPG Cards JSON Builder, Plutonium Features, Changelog, Privacy Policy, external Roll20 Script Help link, generic Help link, Player tools (Stat Generator, This Is Your Life, Names), DM tools (CR Calculator, Encounter Generator, Loot Generator).

---

## Run Locally with Docker (Beginner Friendly)

Follow these steps even if you've never used Docker or a terminal before.

### 1. Install Docker
1. Go to https://www.docker.com/products/docker-desktop/
2. Download Docker Desktop for your operating system (Windows or macOS).
3. Install it using all the default options.
4. Start Docker Desktop and wait until it says "Running" (the whale icon in the system tray/menu bar should stop animating).

### 2. Get the Project Files
If you have not already downloaded this repository:
1. Go to https://github.com/triursa/5e.tools
2. Click the green "Code" button.
3. Choose "Download ZIP".
4. When it finishes downloading, extract (unzip) it to a folder you can find (e.g., your Desktop or Documents).

(If you already cloned with Git, you can skip the ZIP method.)

### 3. Open a Terminal in the Project Folder
Windows:
1. Open File Explorer and navigate to the folder (e.g., `5e.tools`).
2. Click into the white space inside the folder listing.
3. Type `powershell` and press Enter. (Or Right Click -> "Open in Terminal" if available.)

macOS:
1. Open the `Terminal` app.
2. Type `cd ` (with a space), then drag the project folder into the window and press Enter.

### 4. Build the Docker Image
Run this command (copy/paste it):
```powershell
docker build -t 5etools:local .
```
This downloads a small Linux base image, installs a lightweight web server (lighttpd), and copies the site files into it.

### 5. Run the Container
Choose a port that is free on your computer. Common choices: 8080 or 8000. Example:
```powershell
docker run --rm -p 8080:80 --name 5etools 5etools:local
```
Explanation:
- `--rm` removes the container automatically when you stop it
- `-p 8080:80` maps your computer's port 8080 to the container's internal port 80 (lighttpd listens on 80)
- `--name 5etools` gives it a readable name
- `5etools:local` is the image you built

### 6. View the Site
Open a browser and go to:
```
http://localhost:8080/
```
You should see the 5e.tools interface. The main page is `index.html` but direct deep links like `bestiary.html` also work.

### 7. Stop the Container
In the terminal where it's running, press `Ctrl + C` once. If it does not stop after a second, press it again.

### 8. Make Local Changes and Refresh
If you edit HTML/CSS/JS files locally, you must rebuild to see them inside the container:
```powershell
# Stop the old container (Ctrl + C if still running) then:
docker build -t 5etools:local .
docker run --rm -p 8080:80 --name 5etools 5etools:local
```
Alternatively, for rapid iteration, you can mount the current folder instead of rebuilding each time:
```powershell
docker run --rm -p 8080:80 -v "${PWD}:/var/www/localhost/htdocs" --name 5etools 5etools:dev
```
Create the dev image first (copies dependencies once):
```powershell
docker build -t 5etools:dev .
```
Now changes you make to files will be reflected when you refresh the browser (static files only).

### 9. Troubleshooting
- Port already in use: Try a different left-side number, e.g. `-p 8001:80` then open `http://localhost:8001/`.
- Site not loading: Ensure Docker Desktop is running. Re-run the container command and watch for errors.
- Nothing at `/`: Try `http://localhost:8080/index.html` directly.
- Browser cached old files: Press Ctrl+F5 (hard refresh) or open DevTools and disable cache while DevTools are open.
- Changed files not appearing after rebuild: Confirm the build output shows COPY happening and that you re-ran `docker run`.

### 10. (Optional) Use the Prebuilt Base Image
There is an alternate Dockerfile at `docker/dockerfile/main.Dockerfile` which uses a published base image. To use it:
```powershell
docker build -f docker/dockerfile/main.Dockerfile -t 5etools:base .
docker run --rm -p 8080:80 --name 5etools 5etools:base
```

### 11. Clean Up Disk Space
List images:
```powershell
docker images
```
Remove unused images:
```powershell
docker image prune -f
```

---

## Quick Reference
Build:
```powershell
docker build -t 5etools:local .
```
Run:
```powershell
docker run --rm -p 8080:80 --name 5etools 5etools:local
```
Stop: Ctrl + C in the run terminal.

---
