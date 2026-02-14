# ZenithProxy Villager Trader Plugin

Fork of [rfresh2/ZenithProxyVillagerTrader](https://github.com/rfresh2/ZenithProxyVillagerTrader) with additional features and updated for Minecraft 1.21.11/1.21.10.

Automatically buys and sells items with villagers.

Includes automatic restocking, storing, multiple backup chests, restock waiting, and highly configurable trade options.

## Changes from Upstream

* Updated to Minecraft 1.21.11/1.21.10
* Added restock wait feature - bot pauses and retries when all villagers are out of stock
* Added multiple backup chests - bot sequentially withdraws from backup chests when the primary input chest runs out
* Fixed Discord trade status notifications not triggering during restock wait

## Usage

You need the following setup ingame:

1. A villager trading hall. Its best to be compact - the plugin won't go searching for villagers outside render distance.
1. Chests to restock trade inputs from. You can set up a hopper system to constantly refill the chests.
1. Optionally, multiple backup chests for input items in case the primary chest runs out. The bot will try each backup chest in order.
1. Chests to store the items bought from trades. You can set up a hopper system to transfer items out to larger storage systems.

### Commands

* `trader on/off`
* `trader add <id> <profession> <inputItem1> <outputItem> <inputItem1ChestPos> <outputChestPos>`
  * One input item trades
* `trader add <id> <profession> <inputItem1> <inputItem2> <outputItem> <inputItem1ChestPos> <inputItem2ChestPos> <outputChestPos>`
  * Two input items trades
* `trader set help`
  * Prints many additional trade configuration subcommands, like enchantments, prices, and restock settings
* `trader del <id>`
* `trader clear`
* `trader list`
* `trader waitForInteractionTimeout <ticks>`
* `trader restockWaitTime <ticks>`
  * How long to wait when all villagers are out of stock before retrying (default: 6000 ticks = 5 minutes)
* `trader set <id> backupChests add <x> <y> <z>`
  * Adds a backup chest for input item 1
* `trader set <id> backupChests del <index>`
  * Removes a backup chest by its number (1-based)
* `trader set <id> backupChests list`
  * Lists all configured backup chests
* `trader set <id> backupChests clear`
  * Removes all backup chests

### Actions Loop

This module is intended to be run continuously. 

It will repeatedly attempt all configured trades one at a time.

When all villagers are out of stock, the bot will wait for the configured restock time before retrying.

When the primary input chest runs out, the bot will automatically try each backup chest in order until it has enough items or all chests are exhausted.

## Thanks

Special thanks to @Devin for providing a reference trading module and explanation
