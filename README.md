# VortexLauncher 
import java.util.Scanner;
import java.io.FileOutputStream;
import java.util.zip.ZipEntry;
import java.util.zip.ZipOutputStream;
import java.nio.charset.StandardCharsets;

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        String nickname = "Player";
        String accountType = "Offline";
        String version = "1.21.4";

        while (true) {
            System.out.println("\n===============================");
            System.out.println("     VORTEX LAUNCHER v1.0      ");
            System.out.println("===============================");
            System.out.println("Profile: [" + accountType + "] " + nickname);
            System.out.println("Version: " + version);
            System.out.println("-------------------------------");
            System.out.println("1. Select account type (Offline / Microsoft / Ely.by)");
            System.out.println("2. Enter username");
            System.out.println("3. Select game version");
            System.out.println("4. Create skin resource pack (VortexSkin.zip)");
            System.out.println("5. LAUNCH GAME (MJLauncher)");
            System.out.println("0. Exit");
            System.out.print("Choose action: ");

            String choice = scanner.nextLine();

            if (choice.equals("1")) {
                System.out.print("Enter type (1 - Offline, 2 - Microsoft, 3 - Ely.by): ");
                String acc = scanner.nextLine();
                if (acc.equals("1")) accountType = "Offline";
                else if (acc.equals("2")) accountType = "Microsoft";
                else if (acc.equals("3")) accountType = "Ely.by";
            } else if (choice.equals("2")) {
                System.out.print("Enter new username: ");
                nickname = scanner.nextLine();
                System.out.println("Username saved!");
            } else if (choice.equals("3")) {
                System.out.print("Enter version (e.g. 1.20.1 or 1.16.5): ");
                version = scanner.nextLine();
            } else if (choice.equals("4")) {
                createSkinPack();
            } else if (choice.equals("5")) {
                System.out.println("\n>>> Preparing profile: " + nickname + " (" + accountType + ")");
                System.out.println(">>> Target package: git.artdeell.mjlaunch");
                System.out.println(">>> Ready!");
                break;
            } else if (choice.equals("0")) {
                System.out.println("Exiting launcher...");
                break;
            }
        }
        scanner.close();
    }

    private static void createSkinPack() {
        try {
            FileOutputStream fos = new FileOutputStream("VortexSkin.zip");
            ZipOutputStream zos = new ZipOutputStream(fos);

            String mcmeta = "{\"pack\":{\"pack_format\":15,\"description\":\"VortexLauncher Offline Skin\"}}";
            zos.putNextEntry(new ZipEntry("pack.mcmeta"));
            zos.write(mcmeta.getBytes(StandardCharsets.UTF_8));
            zos.closeEntry();

            zos.close();
            System.out.println("[SUCCESS] VortexSkin.zip created!");
        } catch (Exception e) {
            System.out.println("[ERROR] Failed: " + e.getMessage());
        }
    }
}
