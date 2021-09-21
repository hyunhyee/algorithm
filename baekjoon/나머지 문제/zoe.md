[문제링크] https://www.acmicpc.net/problem/3052

	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
        int[] numbers = new int[10];
        int[] remainder = new int[42];
        int count = 0;
        
        for(int i = 0; i<numbers.length; i++) {
        	int number = sc.nextInt();
        	numbers[i] = number%42;
        	remainder[numbers[i]]++;
        }
        
        for(int i=0; i<remainder.length; i++) {
        	if(remainder[i] !=0) {
        		count++;
        	}
        }
        System.out.println(count);
	}
