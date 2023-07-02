
# Running the Repository

## Developing

Once you've created a project and installed dependencies with `npm install` (or `pnpm install` or `yarn`), start a development server:

```bash
npm run dev



# or start the server and open the app in a new browser tab
npm run dev -- --open
```

## Building

To create a production version of your app:

```bash
npm run build
```

You can preview the production build with `npm run preview`.


# Documentation

## File Structure

### Svelte
Each URL is under the src/routes folder.
The main page is directly under the routes folder with the corresponding files +page.svelte +page.js +layout.svelte

The Sub pages are under the correspoding folders with the same fileseg. /projects/+page.svelte and +page.js

The dynamically generated routes (if there are any) are saved under a [slug]/+page.svelte +page.js

Resused components are under src/lib

### JS
The +page.js folder handles the datafetching from the Pocketbase server (running on Hetzner)

The src/lib/utils/getURL.js handels image requests and standadize the URL fetching


### CSS
There is only one +layout.svelte file and it handles all the global css variables (eg. color) and global styles

Each component and +page.svelte has its own css in the down section.

To Do: There is still alot of inline code in the HTML. Needs to be refactored.

Important to remember: Local css variables override the global once and inline css variables override the local ones


## Database

### Pocketbase

The admin interface to the Pocketbase is: https://pocketbase.telesis.at/_/


### Routes

![image](https://github.com/telesisGmbH/telesis.website.svelte/assets/10091040/7349b0f0-22cc-4056-b4ce-9e5260d528fb)

Pb-Name        -      Code-Name      -    Name-Tag

categories     -      categories     -    Services

companies      -     collaborations   -  collaborations

news       -          news      -         news      -    (disabled for now)

pages        -        src/routes     -    pagenames     

projects      -       projects      -     projects

team         -        team         -      team


Pages:

![image](https://github.com/telesisGmbH/telesis.website.svelte/assets/10091040/5a45d8eb-7306-4fe2-8152-042a2707532f)

The Pages folder in Code contains all the Main Pages of the Website.

## Usage

Dynamically routed pages generate elements on their own when you add them to the database.

Dynamic Content:

companies

categories

news

projects

team

Static Pages need to be coded manually

Static Content:

pages


### Add items

With the +New record Button you cann add a new record in the database you are currently in.

Each element got its own datapoints and will be handled differently.

![image](https://github.com/telesisGmbH/telesis.website.svelte/assets/10091040/4c9cefad-3b3b-4061-9519-f60371450ad6)

Most of the Records got a Rich-Text-Element that you can use like a Word processing program. It will render the content how you pasted it inside the editor.

![image](https://github.com/telesisGmbH/telesis.website.svelte/assets/10091040/d87b0145-93a4-4344-ac2a-922756a106bb)

Use the Add Image button to add Images the the Rich-Text. You can set up the width and height there.

![image](https://github.com/telesisGmbH/telesis.website.svelte/assets/10091040/3910a6ad-2b4c-4752-86a7-c8adc313f5b0)


### Removing items

For removing the Items you need to select one and a new option appears.

![image](https://github.com/telesisGmbH/telesis.website.svelte/assets/10091040/96134a3c-1cff-4bf7-8be6-c38ae20ccfc3)



