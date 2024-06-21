# WorldQuest
Private Project for MMO Insperation for Minecraft Server
package com.yourplugin;

import org.bukkit.plugin.java.JavaPlugin;

public class WorldQuest extends JavaPlugin {

    private static WorldQuest instance;
    private ConfigManager configManager;
    private CommandHandler commandHandler;
    private EventListener eventListener;
    private DatabaseManager databaseManager;

    @Override
    public void onEnable() {
        instance = this;
        
        // Initialize managers
        configManager = new ConfigManager(this);
        commandHandler = new CommandHandler(this);
        eventListener = new EventListener(this);
        databaseManager = new DatabaseManager(); // Initialize your database manager

        // Load configurations
        configManager.loadConfigurations();

        // Register commands
        commandHandler.registerCommand("worldquest", new WorldQuestCommandExecutor());

        // Register events
        getServer().getPluginManager().registerEvents(eventListener, this);

        getLogger().info("WorldQuest has been enabled.");
    }

    @Override
    public void onDisable() {
        // Save configurations
        configManager.saveConfigurations();

        getLogger().info("WorldQuest has been disabled.");
    }

    public static WorldQuest getInstance() {
        return instance;
    }

    public ConfigManager getConfigManager() {
        return configManager;
    }

    public CommandHandler getCommandHandler() {
        return commandHandler;
    }

    public DatabaseManager getDatabaseManager() {
        return databaseManager;
    }
}
