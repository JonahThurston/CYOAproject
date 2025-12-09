# Final Report

- Source code repo: https://github.com/JonahThurston/odyssey-game
- Hosted app: https://odyssey-game-74031.web.app/

## Project Summary

This project is a web-hosted, text-based, choose your own adventure game loosely inspired by Homer's Odyssey. It was written in Angular, and is hosted on Google's firebase service, using firestore for the database. It features a handcrafted story, made with the goal of having player choices matter significantly.

## Diagram (ERD)

<img width="1089" height="808" alt="image" src="https://github.com/user-attachments/assets/d563dc78-6e12-4d69-b57f-3b94da4bdf65" />

### ERD explantion

This diagram shows the structure of the data that this site needs to operate.
The top five tables show the data that makes up the story of the game. These are not writable and will remain completely static, and read-only, once the story is fully written.
- Quests: The player will traverse through many quests. These can be thought of as Chapters, contained sub-arcs of the story. Right now, only the prologue quest is written.
- Scenes: Each quest has many scenes. A scene is all of the story neccessary to set up the next choice the player needs to make.
- Messages: Each scene has many messages. These messages are dialogue or narration that informs the player of the situation they are in before they must select a choice.
- Choices: Each scene has many choices. These choices contain a bit of text that describes to the player what options the player character has available to them in the given scene. Choices can be locked behind certain requirements (for instance, they may not be able to choose to fire a canon if they do not have the requisite ammunition resource or the gunnery skill).
- NavInfo: Each scene has an associated navigation info. This just contains the neccessary information to keep track of how exactly a player navigated to a particular scene. This way, the system can roll back the effects of taking certain choices if the player decides to undo a choice.

The bottom three tables show the data that makes up the state of each users' game. This functionality is currently under development, but eventually it will be a writable save system, so player's can maintain their progress
- Users: Each user is given their own entry on the user table. This keeps track of what quest and scene the user is on, as well as the stack of NavInfo they have taken to get there (allowing them to undo their choices).
- Flags: Each user has many flags. These are boolean values that are set to keep track of important choices the player has made. For instance, if the player chooses to spare their nemesis, a "Spared" flag might be set. This way the story can react to those developments.
- Inventory: Each user has many inventory items. These are numeric values tied to item names. For instance, over the course of the game the player may collect 7 Munitions for them to use later. 

## Demo Images

### Home screen:
<img width="1916" height="906" alt="image" src="https://github.com/user-attachments/assets/35560b25-87bc-4f73-ac4d-8c97cff4ff42" />

This screen will eventually be where users are able to authenticate, and thus access their saved user data. Because that functionality is still under development, the only button that is currently enabled is to start a new game.

### First scene:
<img width="1919" height="911" alt="image" src="https://github.com/user-attachments/assets/d471bfa5-256c-492f-817e-fc3d055a7258" />

This scene is the start of the story. Notice the messages in the middle of the screen, and the choices below them. Also notice all of the different inventory items on the left and right side of the screen. 

### Making a choice:
<img width="1919" height="909" alt="image" src="https://github.com/user-attachments/assets/b9480fa2-a2fb-4381-8e7e-205819413f2d" />

All of those choices are valid, but for this demo, I chose the "Pick up the pace" option. You can see that it retrieved the associated scene from the database, with new messages and new choices. It also adjusted the "wit" and "physicality" inventory items. Additionally, there is now an undo button on the far right side, which will successfully revert to the previous scene and undo the inventory effects.

## What did I learn

I learned a ton from this project! Obviously, the primary thing I learned was just how to use Angular. I had not really worked in it extensively before, but wanted to familiarize myself with it for my upcoming job. I also learned how to use firebase web hosting as well as firestore databases. Originally, I had planned to use Supabase, but had run into super odd buggs and CORS issues. I guess that means I also learned what a CORS issue was. 

More abstractly, I also learned a lot about the process and challenges of making a large project like this. I struggled a lot more than I thought I would to get all the different technologies hooked together and functional. I felt like I understood them all just fine seperately, and didn't expect integrating them to be as difficult as it was.

## AI usage

I did not use any AI in this project. I did consider that it could be really cool to have an AI generate the messages and choices. This would allow the story to essentially run infinitely, and by sending it the flags and inventory with every generation request, the AI should do pretty good and not forgetting important context. However, I decided not to do this because a large part of the fun of this project was the generation of the story. I had a really great time developing the overearching plot and characters with my brother. And I do think that this way, the story is better able to have a well developed theme, arch, and message than an AI would be able to do through the course of several scene generations. 

## Why this project interests me

This project interests me for several reasons. The first one is just that I love choose your own adventure games, and have since I was a kid. I just really enjoy the concept of collaborative story telling. The player works together with the developer to tell the story they want to tell, and I think thats so rad!!! I also really love the Odyssey and have always wanted to give my own take on a character focused ship journey. Finally, I just love making stateful websites.

## 3 Key learnings

- Angular
- Firebase and firestore
- CORS and general tech integration debugging techniques

## Scalability

This project should scale really well, because I am using the pay as you go plan for firebase and firestore. Right now I only spend a few cents a month on it, but if it ever got popular, it would automattically scale up for a higher cost. I set it to send me an email if it every tries to go beyond a few bucks a month.
