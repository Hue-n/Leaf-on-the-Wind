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
- Sole programmer of the game

- Finite-State Machine Game Manager
```C#

public enum GameStates
    { 
        main_menu,
        paused,
        playing,
        game_over,
        get_back_up
    }
    
// This Finite State Machine Manages all of the Game's States through a switch statement
    
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
    
```

- Dynamic Difficulties
```C#
public enum DifficultyStates
{
    level1,
    level2,
    level3,
}

// in Update();

switch (currentDifficulty)
        {
            case DifficultyStates.level1:
                CurrentScoreTest();
                SetDifficulty(-5);
                spawner.UpdateDifficulty(3);
                break;

            case DifficultyStates.level2:
                CurrentScoreTest();
                SetDifficulty(-40);
                spawner.UpdateDifficulty(2);
                break;

            case DifficultyStates.level3:
                CurrentScoreTest();
                SetDifficulty(-80);
                spawner.UpdateDifficulty(1.5f);
                break;
        }

// Difficulty is bound to the player's current score:

public void CurrentScoreTest()
    {
        if (scoreCount < 50)
            currentDifficulty = DifficultyStates.level1;
        if (scoreCount > 50 && scoreCount < 100)
            currentDifficulty = DifficultyStates.level2;
        if (scoreCount > 100 && scoreCount < 200)
            currentDifficulty = DifficultyStates.level3;
    }
    
// Difficulty is set through a function that takes a speedLimiter float argument:

void SetDifficulty(float speedLimiter)
    {
        ClampDifficulty(speedLimiter);
        scrollSpeed -= speedIncreasePerSecond * Time.deltaTime;
        pointsPerSecond = Mathf.Abs(scrollSpeed) / 2;
    }
```

- Dynamic Obstacle Spawner
```C#

void Update()
    {
        switch (currentMasterSpawnerState)
        {
            case (MasterSpawnerStates.disabled):
                break;
            case (MasterSpawnerStates.enabled):
            
// If the time between spawns is less than or equal to zero, the spawner will randomize an accessor between one and two and use it to instantiate an obstacle at its
// proper spawner. It will then set the time between spawns back to its initial value.

                if (timeBtwSpawn <= 0)
                {
                    int i = Random.Range(0, 2);
                    Debug.Log(i);
                    Instantiate(obstacles[i], spawners[i].position, Quaternion.identity);
                    timeBtwSpawn = startTimeBtwSpawn;
                }

                else
                {
                    timeBtwSpawn -= Time.deltaTime;
                }
                break;
        }
    }

// This function is utilized to update the new spawn time and is updated in the Switch function of the difficulty manager to change the difficulty of the game.

public void UpdateDifficulty(float newSpawnSpeed)
    {
        startTimeBtwSpawn = newSpawnSpeed;
    }
```
