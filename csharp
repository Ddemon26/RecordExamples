using System;
using UnityEngine;

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
