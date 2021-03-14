## Welcome to Leaf on the Wind! A Game Jam Project

### Game Jam Theme: New Beginnings

### Project Description
Leaf on the Wind is an endless runner created for a Game Jam in Unity 2020.1.17f1! You play as a Young Boy running in the woods sliding under branches and jumping over rocks. If you collect any of the leaves that fall periodically from the trees above, you gain another point of health! If the young boy runs out of health, he will fall and cry. But don't worry! There's always an option to get back up! There's always a chance at a New Beginning!

### Resolution
1920 x 1080px

### Controls <br />
F11: Fullscreen (Recommended as it uncovers your score in the top left corner)<br />
A/D: Run Horizontally  <br />
W: Jump  <br />
Space: Slide  <br />

Tip: You're able to cancel your jump into a slide by pressing "Space" mid-jump!

Play the game [here](https://hue-n.github.io/Leaf-on-the-Wind/)!

### Credits:
Hue-n: Lead Programmer, Technical Artist <br />
Alan: Lead Game Designer, Art Director <br />
Tofu: Star Composer, Technical Designer <br />
Rada: Lead Artist, Lead Animator <br />

### Hue-n's Contributions
- Finite-State Machine Game Manager
`    public enum GameStates
    { 
        main_menu,
        paused,
        playing,
        game_over,
        get_back_up
    }
    
    ...
    
     void Update()
    {
        switch (currentGameState) {
            case GameStates.main_menu:
                MainMenu();
                break;
            case GameStates.paused:
                Pause();
                break;
            case GameStates.playing:
                leafSpawnSystem.UpdateLeafSpawnState(LeafSystemStates.enabled);
                Playing();
                break;
            case GameStates.game_over:
                leafSpawnSystem.UpdateLeafSpawnState(LeafSystemStates.disabled);
                GameOver();
                break;
            case GameStates.get_back_up:
                GetBackUp();
                UpdateGameState(GameStates.playing);
                break;
        }
    }
    `
