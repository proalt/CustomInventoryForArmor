package tutorial;

import java.io.File;
import net.minecraft.init.Items;
import net.minecraft.item.Item;
import net.minecraft.item.ItemStack;
import net.minecraft.item.crafting.CraftingManager;
import net.minecraftforge.common.MinecraftForge;
import net.minecraftforge.common.config.Configuration;
import net.minecraftforge.common.util.EnumHelper;
import tutorial.item.ItemUseMana;
import tutorial.network.PacketPipeline;
import cpw.mods.fml.common.Mod;
import cpw.mods.fml.common.Mod.EventHandler;
import cpw.mods.fml.common.Mod.Instance;
import cpw.mods.fml.common.SidedProxy;
import cpw.mods.fml.common.event.FMLInitializationEvent;
import cpw.mods.fml.common.event.FMLPostInitializationEvent;
import cpw.mods.fml.common.event.FMLPreInitializationEvent;
import cpw.mods.fml.common.network.NetworkRegistry;
import cpw.mods.fml.common.registry.EntityRegistry;
import cpw.mods.fml.common.registry.GameRegistry;

@Mod(modid = "tutorial", name = "Tutorial", version = "1.7.2-1.0.0")
public final class TutorialMain
{
	@Instance("tutorial")
	public static TutorialMain instance;

	@SidedProxy(clientSide = "tutorial.ClientProxy", serverSide = "tutorial.CommonProxy")
	public static CommonProxy proxy;

	/** Updated PacketHandler from Forge wiki tutorial: http://www.minecraftforge.net/wiki/Netty_Packet_Handling */
	public static final PacketPipeline packetPipeline = new PacketPipeline();

	/** This is used to keep track of GUIs that we make*/
	private static int modGuiIndex = 0;

	/** Custom GUI indices: */
	public static final int
	GUI_CUSTOM_INV = modGuiIndex++,
	GUI_ITEM_INV = modGuiIndex++;

	/** This is the starting index for all of our mod's item IDs */
	private static int modEntityIndex = 0;

	// MISC ITEMS
	public static Item
	useMana;
	
	@EventHandler
	public void preInit(FMLPreInitializationEvent event) {
		Configuration config = new Configuration(new File(event.getModConfigurationDirectory().getAbsolutePath() + "/Tutorial.cfg"));
		config.load();
		config.save();
	
		useMana = new ItemUseMana().setUnlocalizedName("use_mana");
		GameRegistry.registerItem(useMana, useMana.getUnlocalizedName());
	}

	@EventHandler
	public void load(FMLInitializationEvent event) {
		packetPipeline.initialise();
		proxy.registerRenderers();
		MinecraftForge.EVENT_BUS.register(new TutEventHandler());
		NetworkRegistry.INSTANCE.registerGuiHandler(this, new CommonProxy());
	}

	@EventHandler
	public void postInitialise(FMLPostInitializationEvent event) {
		packetPipeline.postInitialise();
		
		// this is generally a good place to modify recipes or otherwise interact with other mods
	}
}
