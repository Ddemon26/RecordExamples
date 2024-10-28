# C# Record Examples For Unity 

[![Join our Discord](https://img.shields.io/badge/Discord-Join%20Us-7289DA?logo=discord&logoColor=white)](https://discord.gg/knwtcq3N2a)

## Getting Started

To begin working with this repository, follow these steps:

1. **Clone the repository**:
    ```sh
    git clone https://github.com/Ddemon26/RecordExamples.git
    ```

2. **Open in Unity**: Use Unity Hub or the Unity Editor to open the project.

3. **Explore the Examples**: Browse through the examples to understand how C# records can be effectively used in different game development scenarios.

## Overview

The **RecordExamples** repository demonstrates how to use **C# Records** effectively in Unity game development. Records are powerful, immutable data structures that improve code readability, maintainability, and safety—making them ideal for preventing unintended modifications to game data. This repository is geared towards Unity developers looking to leverage records for efficient and reliable data management.

## Why Use C# Records in Unity?

- **Immutability**: Records inherently support immutability, meaning once an object is created, its state cannot be changed. This ensures data consistency and prevents unintended side effects.
- **Simplicity**: With records, developers can create concise data models with less boilerplate code, making data handling simpler and more efficient.
- **Maintainability**: Records lead to cleaner, more reliable code, reducing bugs and making maintenance easier over time.

## Key Concepts Demonstrated

The repository provides examples of how to use records in Unity across different levels of complexity, highlighting:

- **Immutability**: Ensuring data consistency throughout the lifecycle of game objects.
- **Data Modeling**: Structuring data effectively for game systems like inventory, player states, and events.
- **Event-Driven Systems**: Leveraging records for immutably defined events, supporting a clean and dependable event-driven architecture.

## Example Overview
<details>
<summary><strong>Concept</strong></summary>

```csharp
public class StructVsRecordComparer : MonoBehaviour
{
    // Define a simple struct
    // Structs are value types, meaning they are copied by value.
    // This makes structs useful for small, lightweight data that you want to be copied by data rather than reference.
    public struct PlayerStatsStruct
    {
        public int Health { get; }  // Struct properties are immutable due to the readonly nature.
        public int AttackPower { get; }

        public PlayerStatsStruct(int health, int attackPower)
        {
            Health = health;
            AttackPower = attackPower;
        }

        // Explicit comparison method for struct
        // Structs do not have built-in equality methods, so we must manually implement the Equals method.
        public override bool Equals(object obj)
        {
            if (obj is PlayerStatsStruct other)
            {
                return Health == other.Health && AttackPower == other.AttackPower;
            }
            return false;
        }

        // Override GetHashCode for consistent behavior when used in collections
        // This ensures structs with the same data produce the same hash code.
        public override int GetHashCode()
        {
            return HashCode.Combine(Health, AttackPower);
        }

        // ToString for display purposes
        // Provides a human-readable string representation of the struct.
        public override string ToString()
        {
            return $"PlayerStatsStruct(Health: {Health}, AttackPower: {AttackPower})";
        }
    }

    // Define a record
    // Records are reference types, similar to classes, but are designed to be immutable and have built-in equality checks.
    // Records come with several automatically generated methods, including:
    // - Equals: Provides a value-based equality comparison.
    // - GetHashCode: Generates a consistent hash code based on the values of all properties.
    // - ToString: Automatically generates a human-readable string representation of the record.
    public record PlayerStatsRecord(int Health, int AttackPower);

    void Start()
    {
        // Create instances of struct and record
        var playerStruct1 = new PlayerStatsStruct(100, 50);
        var playerStruct2 = playerStruct1;  // Copy by value
        var playerRecord1 = new PlayerStatsRecord(100, 50);
        var playerRecord2 = playerRecord1;  // Copy by reference

        // Demonstrate struct behavior (copied by value)
        // Structs are value types, so assigning playerStruct1 to playerStruct2 creates an independent copy.
        Debug.Log($"Original Struct: {playerStruct1}");
        playerStruct2 = new PlayerStatsStruct(120, 60);  // Modify the copy
        Debug.Log($"Modified Struct Copy: {playerStruct2}");
        Debug.Log($"Original Struct after modifying copy: {playerStruct1}"); // Original struct remains unchanged

        // Demonstrate record behavior (copied by reference)
        // Records, being reference types, will point to the same memory location when assigned, meaning changes affect all references.
        Debug.Log($"Original Record: {playerRecord1}");
        Debug.Log($"Copied Record Reference: {playerRecord2}");
        Debug.Log($"Are playerRecord1 and playerRecord2 equal? {playerRecord1 == playerRecord2}"); // True because records compare by value
        
        // Since records are immutable, to "modify" we create a new instance using 'with'
        // The 'with' keyword allows you to create a new record with modified values while keeping the original intact.
        var modifiedRecord = playerRecord1 with { Health = 150 };
        Debug.Log($"Modified Record (with new value): {modifiedRecord}");
        Debug.Log($"Original Record remains unchanged: {playerRecord1}");

        // Demonstrate immutability of structs and records
        // Copying a struct creates a new independent instance, which means changes to the copy do not affect the original.
        var structCopy = playerStruct1;
        structCopy = new PlayerStatsStruct(150, 75);  // Modify the copy
        Debug.Log($"Original Struct after modifying structCopy: {playerStruct1}"); // Original struct remains unchanged
        Debug.Log($"Modified Struct Copy: {structCopy}");

        // Copying a record creates a new reference to the same instance, which means both point to the same data.
        var recordCopy = playerRecord1;
        Debug.Log($"Original Record: {playerRecord1}");
        Debug.Log($"Copied Record Reference: {recordCopy}");
        
        // Since records are immutable by default, modifying a copy requires creating a new record using the 'with' keyword.
        var modifiedRecordCopy = recordCopy with { AttackPower = 75 };
        Debug.Log($"Modified Record Copy (with new value): {modifiedRecordCopy}");
        Debug.Log($"Original Record remains unchanged: {playerRecord1}");
    }
}
```
</details>

<details>
<summary><strong>High-Level Examples</strong></summary>

### Abstract Event Bus
Records are used to define data structures for an event bus system, ensuring events are immutable after creation. This reduces complexity and decouples different components, making the system easier to maintain.

```csharp
using System;
using UnityEngine;

namespace TCS
{
    // Define an enumeration for event types
    enum EventType { ItemPickup, BossFight, ExperienceGain }

    // Define a record for GameEvent to ensure immutability
    record GameEvent(int EventID, EventType Type, DateTime EventTime);

    public class GameEventExample : MonoBehaviour
    {
        private void Start()
        {
            // Create an instance of a GameEvent
            GameEvent newEvent = new GameEvent(1, EventType.BossFight, DateTime.Now);

            // Log the game event details
            Debug.Log($"Event ID: {newEvent.EventID}, Type: {newEvent.Type}, Time: {newEvent.EventTime}");
        }
    }
}
```

Highlighted the purpose of the `Start` method for creating and logging the event.

### Friend Request Management
The **FriendRequest** example demonstrates how to use records to manage friend requests. The immutability of records guarantees that friend request data remains consistent, reducing the chances of accidental modifications during user interactions.

</details>

<details>
<summary><strong>Mid-Level Examples</strong></summary>

### Achievements and Player Progression
Records are used in the **Achievements** and **Player Progression** examples to keep track of player achievements and progress. Immutability ensures that data like levels, experience, and badges remain consistent, reducing potential errors.

### Inventory System
The **InventoryItem** record is used to represent items in a player’s inventory, such as consumables or equipment. This guarantees that inventory data cannot be modified without intention, providing stability to the system.

```csharp
namespace TCS.Tests.RecordExamples
{
    // Define an InventoryItem record to represent items in a player's inventory immutably
    public record InventoryItem(string Name, int ID, int Quantity);

    public class InventoryManager : MonoBehaviour
    {
        private void Start()
        {
            // Create a new InventoryItem instance
            InventoryItem item = new InventoryItem("Health Potion", 1, 3);

            // Log the item details to demonstrate usage
            Debug.Log($"Item Name: {item.Name}, ID: {item.ID}, Quantity: {item.Quantity}");

            // Note: item.Quantity cannot be modified directly due to record's immutability
        }
    }
}
```


### Trade Manager
The **TradeManager** uses records to model trade transactions, ensuring data integrity. The use of records ensures that all trade data remains consistent and cannot be accidentally altered.

```csharp
using UnityEngine;
using System;
using System.Collections.Generic;

namespace TCS
{
    public class TradeManagerExample : MonoBehaviour
    {
        // Define a record to represent a trade transaction
        public record TradeTransaction(string PlayerName, string NpcName, Item PlayerItem, Item NpcItem, DateTime TransactionTime);

        // Define a record to represent an item
        public record Item(string Name, int ID);

        // Define a record to represent a trade offer
        public record TradeOffer(Item OfferedItem, Item RequestedItem, string TraderName);

        // A list to store all trade transactions
        private readonly List<TradeTransaction> m_transactionHistory = new List<TradeTransaction>();

        private void CompleteTrade(TradeOffer offer, Item playerItem)
        {
            if (playerItem != null)
            {
                // Log transaction as a record to maintain data consistency
                var transaction = new TradeTransaction(
                    PlayerName: "Player1",
                    NpcName: offer.TraderName,
                    PlayerItem: playerItem,
                    NpcItem: offer.OfferedItem,
                    TransactionTime: DateTime.Now
                );

                // Add the completed transaction to history
                m_transactionHistory.Add(transaction);

                Debug.Log($"Trade completed! Received {offer.OfferedItem.Name} for {playerItem.Name} from {offer.TraderName}.");
            }
            else
            {
                Debug.Log($"Trade failed. Player does not have the requested item: {offer.RequestedItem.Name}");
            }
        }
    }
}
```


</details>

<details>
<summary><strong>Low-Level Examples</strong></summary>

### AI Settings
The **AISettings** record encapsulates AI behavior data like patrol range, detection radius, and aggressiveness level. Using records guarantees that these settings remain consistent throughout runtime, making AI behaviors more predictable.

```csharp
using UnityEngine;

namespace TCS
{
    public class AISettingsExample : MonoBehaviour
    {
        // Define AI settings using a record to enforce immutability
        record AISettings(float PatrolRange, float DetectionRadius, int AggressivenessLevel);

        // Create a readonly instance of AISettings to demonstrate immutability
        readonly AISettings settings = new AISettings(10.0f, 5.0f, 3);

        private void Start()
        {
            // Log the AI settings to demonstrate usage
            Debug.Log($"Patrol Range: {settings.PatrolRange}, Detection Radius: {settings.DetectionRadius}, Aggressiveness Level: {settings.AggressivenessLevel}");

            // Trying to change the settings here will throw an error due to immutability.
        }
    }
}
```


### Game Difficulty Settings
The **GameDifficultySettings** example uses records to define settings like enemy spawn rates and player damage multipliers. This ensures that difficulty levels remain consistent throughout the game, reducing unintended gameplay variations.

### Game Events
The **GameEvent** example shows how to use records to define different game events like `ItemPickup`, `BossFight`, and `ExperienceGain`. By making events immutable, the code becomes more reliable and easier to debug.

```csharp
using System;
using UnityEngine;

namespace TCS
{
    public class GameEventExample : MonoBehaviour
    {
        enum EventType { ItemPickup, BossFight, ExperienceGain }
        record GameEvent(int EventID, EventType Type, DateTime EventTime);

        private void Start()
        {
            GameEvent newEvent = new GameEvent(1, EventType.BossFight, DateTime.Now);
            Debug.Log($"Event ID: {newEvent.EventID}, Type: {newEvent.Type}, Time: {newEvent.EventTime}");
        }
    }
}
```

</details>

## Practical Usage Examples

<details>
<summary><strong>Inventory Example</strong></summary>

This example uses the **InventoryItem** record to manage player inventory items:

```csharp
InventoryManager inventory = new InventoryManager();
InventoryItem item = new InventoryItem("Health Potion", 1, 3);
inventory.AddItem(item);
```

The immutability of **InventoryItem** ensures that once an item is created, its properties cannot be changed unintentionally.

</details>

<details>
<summary><strong>Event Bus Example</strong></summary>

The **AbstractEventBus** example demonstrates how records can be used for event data, promoting safe and immutable communication between game components:

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

</details>

<details>
<summary><strong>AI Settings Example</strong></summary>

The **AISettings** record is used to define AI behaviors in an immutable way:

```csharp
AISettings settings = new AISettings(10.0f, 5.0f, 3);
Debug.Log("AI Patrol Range: " + settings.PatrolRange);
```

This ensures that AI configuration remains stable throughout the game lifecycle.

</details>

## Contributing

We welcome contributions to enhance this repository! To contribute:

1. **Fork the repository**.
2. **Create a new branch** (`git checkout -b feature-branch`).
3. **Commit your changes** (`git commit -m 'Add new feature'`).
4. **Push to the branch** (`git push origin feature-branch`).
5. **Open a pull request**.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Community

Join our Discord community to ask questions, share ideas, or collaborate:

[![Join our Discord](https://img.shields.io/badge/Discord-Join%20Us-7289DA?logo=discord&logoColor=white)](https://discord.gg/knwtcq3N2a)

We look forward to collaborating with you!

