# RecordExamples Repository

[![Join our Discord](https://img.shields.io/badge/Discord-Join%20Us-7289DA?logo=discord&logoColor=white)](https://discord.gg/knwtcq3N2a)
![Discord](https://img.shields.io/discord/1047781241010794506)

![GitHub Forks](https://img.shields.io/github/forks/Ddemon26/RecordExamples)
![GitHub Contributors](https://img.shields.io/github/contributors/Ddemon26/RecordExamples)
![GitHub Stars](https://img.shields.io/github/stars/Ddemon26/RecordExamples)
![GitHub Repo Size](https://img.shields.io/github/repo-size/Ddemon26/RecordExamples)

## Overview

The **RecordExamples** repository demonstrates the usage of **C# Records** in Unity to implement various game-related features, organized into three levels of complexity: **High-Level**, **Mid-Level**, and **Low-Level**. This repository is designed to serve as a reference for developers seeking to leverage the new C# **record** type for more concise and immutable data structures in their Unity projects. It features several C# scripts showcasing how to use records to simplify data management for features like inventory systems, quests, AI configurations, game events, player progression, and more.

The goal of this repository is to present a clear and structured approach to utilizing C# records in Unity, making it easy for developers to learn and adapt the provided solutions into their projects.

## Repository Structure

This repository is organized into three primary directories, each focusing on a different level of abstraction and implementation:

### 1. High-Level Example
- **AbstractEventBus**: Defines an abstract event bus for handling event-driven communication between different parts of the application, promoting a decoupled architecture that improves scalability and maintainability.
- **FriendRequest**: Manages friend requests, which may be part of a social component in a game or application, allowing users to send, receive, and manage friendships.

### 2. Mid-Level Example
- **Achievements**: Handles achievements and badges that a player can earn, offering a structured way to track player accomplishments and provide feedback.
- **Inventory**: Manages player inventory, tracking items, quantities, and usage, facilitating the core gameplay mechanic of managing resources.
- **PlayerProgression**: Tracks the player's progression, including level, experience, and unlocked content, helping developers implement features related to character growth and story advancement.
- **TradeManager**: Manages trading mechanics, which may include player-to-player trading or interaction with in-game shops, providing players with opportunities to exchange items or currency.

### 3. Low-Level Example
Contains a variety of C# scripts that provide more detailed implementations of core game mechanics, utilizing records for improved readability and immutability:

- **AISettingsExample.cs**: Defines `AISettings` using a record to encapsulate behavior settings, such as patrol range, detection radius, and aggressiveness level, allowing developers to customize AI behaviors easily.
- **GameDifficultySettingsExample.cs**: Implements game difficulty settings, such as enemy spawn rates, maximum enemy count, and player damage multipliers, providing flexibility for adjusting the challenge level of the game.
- **GameEventExample.cs**: Manages game events using enums to define types such as `ItemPickup`, `BossFight`, and `ExperienceGain`. This script shows how different game components can respond to significant occurrences, promoting an event-driven architecture.
- **InventoryItem.cs & InventoryItemExample.cs**: Represents individual inventory items with properties like name, ID, and quantity. The example includes different item types, such as `Weapon`, `Consumable`, and `CraftingMaterial`, showcasing how to manage varied inventory elements using records.
- **InventoryManager.cs**: Implements the inventory system using a dictionary to store items by ID. It supports adding, removing, and managing quantities of items, forming the backbone of the inventory feature used in games.
- **PlayerProfileExample.cs**: Defines `PlayerProfile` as a record, which includes essential player information, such as player name, ID, and age. This helps in managing player-specific settings and preferences concisely.
- **PlayerRecord.cs & PlayerStats.cs**: Handles player statistics, such as health, mana, and strength. `PlayerRecord` manages initial and updated stats, providing a comprehensive view of player progression over time using records.
- **PlayerStateExample.cs**: Defines `PlayerState`, which includes player position, inventory, and other states like health, providing a snapshot of a player's current in-game status. This helps in saving and restoring game progress.
- **QuestExample.cs**: Defines quests with properties like `QuestName`, `Objective`, `Description`, and `Reward`. This class allows developers to implement a quest system where players can complete tasks for rewards using records for simplicity.
- **SkillExample.cs**: Manages player skills, including skill name, damage, cost, cooldown, and description. This class is used for implementing a skill system, helping to define different abilities players can use in combat or other scenarios.

## Key Features
- **Utilizing C# Records in Unity**: This repository demonstrates how to use C# records to make data structures more readable, maintainable, and immutable. Records are ideal for representing simple data models, and this repository shows practical examples of applying them in Unity game development.
- **Event-Driven Architecture**: The **High-Level Example** demonstrates how to use an abstract event bus to decouple different parts of the application, making the codebase more maintainable and scalable.
- **Inventory Management**: Scripts like **InventoryManager.cs** and **InventoryItem.cs** handle all aspects of inventory functionality, such as adding items, tracking quantities, and managing inventory UI interactions using records to simplify data definitions.
- **Player Progression**: **PlayerProfileExample.cs**, **PlayerRecord.cs**, and **PlayerStats.cs** help track the player's journey through the game, including achievements, experience, and levels, facilitating the design of character growth mechanics.
- **AI Settings and Player States**: The **Low-Level Example** provides insights into configuring AI behavior through **AISettingsExample.cs** and managing player state with **PlayerStateExample.cs**, allowing for a more dynamic and responsive gaming experience.
- **Game Events and Difficulty Settings**: **GameEventExample.cs** and **GameDifficultySettingsExample.cs** help manage dynamic aspects of gameplay by responding to in-game events and adjusting difficulty as needed.

## Getting Started
To get started with the **RecordExamples** repository:

1. **Clone the repository**:
    ```sh
    git clone https://github.com/Ddemon26/RecordExamples.git
    ```

2. **Open in Unity**: The repository is designed to work within Unity. Open the project using Unity Hub or from the Unity Editor directly.

3. **Explore Examples**: Navigate through the **HighLevelExample**, **MidLevelExample**, and **LowLevelExample** directories to explore the provided scripts. These scripts are meant to be modular and reusable, allowing you to easily integrate them into your existing projects.

## Usage Examples

### Inventory Example
The **InventoryManager.cs** script can be used to manage player inventory. Here is a quick example of how to add an item to the inventory:

```csharp
InventoryManager inventory = new InventoryManager();
InventoryItem item = new InventoryItem("Health Potion", 1, 3);
inventory.AddItem(item);
```

### Event Bus Example
The **AbstractEventBus** provides a way to communicate between different parts of the game. Here is how to publish and subscribe to an event:

```csharp
public class Player : MonoBehaviour
{
    private void Start()
    {
        EventBus.Subscribe<PlayerDiedEvent>(OnPlayerDied);
    }

    private void OnPlayerDied(PlayerDiedEvent e)
    {
        Debug.Log("Player has died: " + e.PlayerId);
    }
}
```

### AI Settings Example
The **AISettingsExample.cs** script allows developers to define AI behaviors. Here is a quick example:

```csharp
AISettings settings = new AISettings(10.0f, 5.0f, 3);
Debug.Log("AI Patrol Range: " + settings.PatrolRange);
```

## Contributing
Contributions are welcome! If you have examples, features, or improvements you would like to share, please feel free to submit a pull request.

1. Fork the repository.
2. Create a new branch (`git checkout -b feature-branch`).
3. Commit your changes (`git commit -m 'Add new feature'`).
4. Push to the branch (`git push origin feature-branch`).
5. Open a pull request.

## License
This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Contact & Community
If you have any questions or need further assistance, please feel free to join our Discord community using the link below.

[![Join our Discord](https://img.shields.io/badge/Discord-Join%20Us-7289DA?logo=discord&logoColor=white)](https://discord.gg/knwtcq3N2a)

We look forward to collaborating with you!
