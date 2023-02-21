![image](https://user-images.githubusercontent.com/42806772/220437444-1aa13a6b-4a0d-4624-b235-eaaae65d3365.png)

![image](https://user-images.githubusercontent.com/42806772/220437504-4ed63504-bc2d-4bbc-b419-b1b16b8718ca.png)

```java
import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.IOException;
import java.io.InputStreamReader;
import java.io.OutputStreamWriter;
import java.util.PriorityQueue;

public class Main {

	public static void main(String[] args) throws IOException {
		BufferedReader reader = new BufferedReader(new InputStreamReader(System.in));
		BufferedWriter writer = new BufferedWriter(new OutputStreamWriter(System.out));

		int maxWidth = Integer.parseInt(reader.readLine());
		String[] nk = reader.readLine().split(" ");
		long n = Long.parseLong(nk[0]);
		long k = Long.parseLong(nk[1]);

		PriorityQueue<Photo> photos = new PriorityQueue<>();
		PriorityQueue<Photo> photos2 = new PriorityQueue<>();

		for (long i = 0; i < n; i++) {
			String[] p = reader.readLine().split("x");

			int height = Integer.parseInt(p[0]);
			int width = Integer.parseInt(p[1]);

			photos.add(new Photo(height, width));
			photos2.add(new Photo(height, width));
		}

		int max = -0;
		int min = -0;

		for (long i = 0; i < k; i++) {
			Photo best = photos.poll();

			max += Math.ceil(best.getHeight() * maxWidth * 1.0 / best.getWidth());
		}

		while (photos2.size() > k) {
			photos2.poll();
		}

		for (long i = 0; i < k; i++) {
			Photo best = photos2.poll();
			min += Math.ceil(best.getHeight() * maxWidth * 1.0 / best.getWidth());
		}

		writer.write(min + "\n");
		writer.write(String.valueOf(max));

		reader.close();
		writer.close();
	}
}

class Photo implements Comparable<Photo> {

	private int width;
	private int height;
	private Double effectivity;

	public Photo(int width, int height) {
		this.width = width;
		this.height = height;
		this.effectivity = height * 1.0 / width;
	}

	public int getWidth() {
		return width;
	}

	public void setWidth(int width) {
		this.width = width;
	}

	public int getHeight() {
		return height;
	}

	public void setHeight(int height) {
		this.height = height;
	}

	public Double getEffectivity() {
		return effectivity;
	}

	@Override
	public int compareTo(Photo o) {
		return -effectivity.compareTo(o.getEffectivity());
	}
}
```
