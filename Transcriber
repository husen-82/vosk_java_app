
import org.vosk.Model;
import org.vosk.Recognizer;
import org.vosk.LibVosk;

import javax.sound.sampled.*;
import java.io.*;

public class Transcriber {
    public static void transcribe(File wavFile) throws Exception {
        LibVosk.setLogLevel(0); // ログ非表示（任意）
        Model model = new Model("model"); // 解凍したモデルフォルダ名

        AudioInputStream ais = AudioSystem.getAudioInputStream(wavFile);
        AudioFormat baseFormat = ais.getFormat();

        // PCM 16bit/Mono に変換
        AudioFormat targetFormat = new AudioFormat(16000, 16, 1, true, false);
        AudioInputStream din = AudioSystem.getAudioInputStream(targetFormat, ais);

        Recognizer recognizer = new Recognizer(model, 16000.0f);
        byte[] buffer = new byte[4096];
        int nbytes;

        System.out.println("文字起こし中...");
        while ((nbytes = din.read(buffer)) >= 0) {
            if (recognizer.acceptWaveForm(buffer, nbytes)) {
                System.out.println(recognizer.getResult());
            }
        }
        System.out.println(recognizer.getFinalResult());
    }
}
