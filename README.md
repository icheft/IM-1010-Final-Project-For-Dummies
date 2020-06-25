# IM 1010 Final Project for Dummies 
FYI, the term "for dummies" does not indicate that you are dummies. Instead, it represents the simplicity of the repo and instructions are well laid.

- [IM 1010 Final Project for Dummies](#im-1010-final-project-for-dummies)
  - [Terminal Basics](#terminal-basics)
  - [How to Use](#how-to-use)
    - [Rendering](#rendering)
  - [Reference](#reference)
  - [Contributions](#contributions)

## Terminal Basics
+ `cd <folderName>`: go to the folder
+ `cd ..`: go back to the previous folder
+ `make`: compile and run in `Grading\` folder
+ `./snake.out <yourName>`: show result

## How to Use
1. Change content in `Snake.cpp` and `Snake.h`.
2. If you want to move both `Snake.cpp` and `Snake.h` to the `Grading/` folder, type `cmd + j` first and enter `sh move.sh`. (type `cd Grading` afterwards)
3. Alternatively, you can just copy and paste the content below `// Add anything else you need` and paste it to the `Snake.cpp` file in `Grading/` folder. Also, make sure you do include:
    ```cpp
    #include <iostream>
    #include <unistd.h>

    void showMap(vector<vector<int>> map); // in public:
    ```
    in the `Snake.h` file in `Grading/` folder.
4. To zip files, just open terminal and type `sh zip.sh` (you can upload the zip file directly afterwards).


### Rendering
In `Grading/main.cpp`. Located from line 300 to 303.

## Reference
+ `Grading/Snake.cpp`
```cpp
#include "COLORS.h"
#include "Snake.h"

void Snake::showMap(vector<vector<int>> map)
{
    queue<tuple<int, int>> tmpPos = this->position;
    tuple<int, int> headPos = tmpPos.back();
    tuple<int, int> tailPos = tmpPos.front();

    // this->cleanSnake();
    while (!tmpPos.empty()) {
        if (map[get<0>(tmpPos.front())][get<1>(tmpPos.front())] == -3) return;
        else
            map[get<0>(tmpPos.front())][get<1>(tmpPos.front())] = -3; //REF: [map change]
        tmpPos.pop();
    }
    const int spaceSize = 2;
    cout << "Map size: " << map.size() << " x " << map[0].size() << endl;
    for (int i = 0; i < map.size(); i++) {
        for (int j = 0; j < map[0].size(); j++) {
            if (i == get<0>(headPos) && j == get<1>(headPos)) {
                cout << string(spaceSize, ' ') << RED << "x" << RESET;
            } else if (i == get<0>(tailPos) && j == get<1>(tailPos)) {
                cout << string(spaceSize, ' ') << BLUE << "x" << RESET;
            } else if (map[i][j] == -3) {
                cout << string(spaceSize, ' ') << GREEN << "x" << RESET;
                // REF: [map change]
            } else if (map[i][j] == -1) {
                cout << string(spaceSize - 1, ' ') << BOLDBLACK << map[i][j] << RESET;
            } else if (map[i][j] != 0) {
                cout << string(spaceSize, ' ') << BOLDYELLOW << map[i][j] << RESET;
            } else
                cout << string(spaceSize, ' ') << map[i][j];
        }
        cout << endl;
    }
    return;

    // cin.ignore();
}

// Add anything else you need
```
+ `Grading/Snake.h`
```cpp
#include <iostream>
#include <unistd.h>

void showMap(vector<vector<int>> map); // in public:
```

## Contributions
If you have any questions, please let me know either through the [issue page](https://github.com/icheft/IM-1010-Final-Project-For-Dummies/issues) or direct message. 

Any contributions are welcome. Fork this repository and submit a pull request if you have better solutions.
