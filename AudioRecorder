
import javax.sound.sampled.*;
import java.io.*;

public class AudioRecorder {
    private static final AudioFormat format = new AudioFormat(16000, 16, 1, true, false);
    private static final File file = new File("record.wav");

    public static void startRecording() throws Exception {
        TargetDataLine line = AudioSystem.getTargetDataLine(format);
        line.open(format);
        line.start();
        AudioInputStream ais = new AudioInputStream(line);
        System.out.println("録音中... Enterで停止");
        Thread stopper = new Thread(() -> {
            try {
                AudioSystem.write(ais, AudioFileFormat.Type.WAVE, file);
            } catch (IOException e) { e.printStackTrace(); }
        });
        stopper.start();

        System.in.read();  // Enterで停止
        line.stop();
        line.close();
        System.out.println("録音終了！");
    }
}
