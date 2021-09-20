문제링크
[Google]: https://programmers.co.kr/learn/courses/30/lessons/83201?language=java

```
class Solution {
    public String solution(int[][] scores) {
        String answer = "";
        int size = scores.length;
        StringBuilder stringBuilder = new StringBuilder();
        for(int i = 0; i< size ; i++){
            int scoreSum = 0;
            int max = 0;
            int min = Integer.MAX_VALUE;
            int minCount = 0;
            int maxCount = 0;
            for(int j = 0; j < size ; j++){
                int score = scores[j][i];
                if(score < min){
                    minCount = 0;
                    min = score;
                } else if(score == min)
                    minCount++;
                if(score > max){
                    maxCount = 0;
                    max = score;
                } else if(score == max)
                    maxCount++; 
                scoreSum+=score;
            }
            int myScore = scores[i][i];
            int scoreAvgSize = size;
            boolean except = (myScore == max && maxCount == 0) || (myScore == min && minCount == 0);
            if(except){
                scoreSum-=myScore;
                scoreAvgSize--;
            }
            int scoreAvg = scoreSum/scoreAvgSize;
            String grade = getGradeForScoreAvg(scoreAvg);
            stringBuilder.append(grade);
        }
        return stringBuilder.toString();
    }
    
    String getGradeForScoreAvg(int scoreAvg){
        String grade = "";
        if(scoreAvg >= 90)
            grade = "A";
        else if(scoreAvg >= 80 && scoreAvg < 90)
            grade = "B";
        else if(scoreAvg >= 70 && scoreAvg < 80)
            grade = "C";
        else if(scoreAvg >= 50 && scoreAvg < 70)
            grade = "D";
        else
            grade = "F";
        return grade;
    }
}
```
