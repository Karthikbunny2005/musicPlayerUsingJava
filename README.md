# musicPlayerUsingJava
/*It is a simple music player where you can enter song name , artist name and song duration and you can view song details in terminal. As of now you cannot listen the song you can just see the song details in the terminal.*/
import java.util.LinkedList;
import java.util.Queue;
import java.util.Scanner;

public class musicPlayerUsingQueue {

    static class Song {
        String title;
        String artist;
        int duration; // Duration in seconds

        public Song(String title, String artist, int duration) {
            this.title = title;
            this.artist = artist;
            this.duration = duration;
        }
    }

    public static class SongQueue {
        private Queue<Song> queue;

        public SongQueue() {
            queue = new LinkedList<>();
        }

        public void enqueue(Song s) {
            queue.add(s);
        }

        public Song dequeue() {
            return queue.poll();
        }

        public boolean isEmpty() {
            return queue.isEmpty();
        }

        public void displayQueue() {
            if (queue.isEmpty()) {
                System.out.println("Queue is empty!");
            } else {
                for (Song song : queue) {
                    System.out.println(song.title + " by " + song.artist + " (" + song.duration + " seconds)");
                }
            }
        }
    }

    public static void main(String[] args) {
        SongQueue songQueue = new SongQueue();
        Scanner scanner = new Scanner(System.in);
        int choice;

        while (true) {
            System.out.println("\n1. Add song to queue");
            System.out.println("2. Play next song");
            System.out.println("3. Display queue");
            System.out.println("4. Exit");
            System.out.print("Enter your choice: ");
            choice = scanner.nextInt();
            scanner.nextLine(); // consume newline

            switch (choice) {
                case 1:
                    System.out.print("Enter song title: ");
                    String title = scanner.nextLine();
                    System.out.print("Enter artist name: ");
                    String artist = scanner.nextLine();
                    System.out.print("Enter duration (in seconds): ");
                    int duration = scanner.nextInt();
                    songQueue.enqueue(new Song(title, artist, duration));
                    break;
                case 2:
                    if (!songQueue.isEmpty()) {
                        Song s = songQueue.dequeue();
                        System.out.println("Now playing: " + s.title + " by " + s.artist);
                        try {
                            Thread.sleep(s.duration * 1000); // Simulating song play
                        } catch (InterruptedException e) {
                            e.printStackTrace();
                        }
                    } else {
                        System.out.println("Queue is empty!");
                    }
                    break;
                case 3:
                    songQueue.displayQueue();
                    break;
                case 4:
                    System.out.println("Exiting...");
                    scanner.close();
                    return;
                default:
                    System.out.println("Invalid choice! Please try again.");
            }
        }
    }
}
