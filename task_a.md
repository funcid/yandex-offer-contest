![image](https://user-images.githubusercontent.com/42806772/220436914-dc3e8351-5f79-4ee2-a061-2f2a46a659f4.png)

![image](https://user-images.githubusercontent.com/42806772/220436984-64dd27ba-f1e6-4793-81c8-f8bc7c039074.png)

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

		String[] sbm = reader.readLine().split(" ");

		long s = Long.parseLong(sbm[0]);
		long b = Long.parseLong(sbm[1]);

		PriorityQueue<Trunk> trunks = new PriorityQueue<>();

		String[] trunkString = reader.readLine().split("\\s+");

		for (String trunk : trunkString) {
			trunks.add(new Trunk(Long.parseLong(trunk)));
		}

		int counter = 0;

		while (s != 0 || b != 0) {

			if (trunks.isEmpty()) {
				writer.write("-1");

				reader.close();
				writer.close();
				return;
			}

			Trunk max = trunks.poll();

			while (max.getMass() >= 50 && b > 0) {
				max.setMass(max.getMass() - 50);
				b--;
			}

			while (max.getMass() >= 10 && s > 0) {
				max.setMass(max.getMass() - 10);
				s--;
			}

			counter++;
		}

		writer.write(String.valueOf(counter));

		reader.close();
		writer.close();
	}
}

class Trunk implements Comparable<Trunk> {

	private Long mass;

	public Trunk(Long mass) {
		this.mass = mass;
	}

	public Long getMass() {
		return mass;
	}

	public void setMass(Long mass) {
		this.mass = mass;
	}

	@Override
	public int compareTo(Trunk o) {
		return -mass.compareTo(o.mass);
	}
}
```
