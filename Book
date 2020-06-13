import java.io.*;
import java.io.FileNotFoundException;
import java.io.IOException;
import java.util.*;


public class Book {
    public static void main(String[] args) {
        if (args.length != 1) {
            System.out.println("USAGE: java Book input.txt");
            System.exit(0);
        }

        String filename = args[0];
        File file = new File(filename);

        // words array
        ArrayList<String > wordsArr = new ArrayList<String>();
        try {
            //read the file
            Scanner fin = new Scanner(file);
            // count characters, words and lines
            int chars = 0, words = 0, lines = 0;
            // text contents
            String contents = "";
            // create is Palindrome array
            ArrayList<String > isP = new ArrayList<String>();
            //to count how many words is Palindrome
            int count_isPal = 0;
//            ArrayList<Character> characters = new ArrayList<Character>();
//            int countSymbols =0;

            //to get the date from the file we use while(fin.hasNextLine())
            while (fin.hasNextLine()) {
                // line
                String line = fin.nextLine();
                // the whole text (file)
                contents += line + '\n';
                // to delete the symbols we use replace method
                //System.out.println(line);
                line = line.replace(",","");
                line = line.replace(".","");
                line = line.replace("?","");
                line = line.replace("!","");
                line = line.replace("\"","");
                line = line.replace(":","");
                line = line.replace(";","");
                // TODO: do not count empty lines
                //words array without space (" ")
                String[] word = line.trim().split("\\s+");
                // how many words in the file
                int wordsOnLine = line.trim().split("\\s+").length;
                words += wordsOnLine;

                for (String str : word){
                    wordsArr.add(str.toLowerCase());
//                    System.out.print(str.toLowerCase()+" ");

                    if (isPalindrome(str.toLowerCase())){
                        count_isPal++;
                        isP.add(str.toLowerCase());
                    }
                }
                chars +=line.length();
                lines++;
            }
            // list of all words to find the anagrams
            List<String> inputList = new ArrayList<String>();
            for (String str : wordsArr)
                inputList.add(str);
            // Set of Anagrams
            Set<String> AnagramArr = new HashSet<String>();
            for (int i = 0; i < inputList.size() - 1; i++) {
//                System.out.println(list);
                for (int j = i + 1; j < inputList.size(); j++) {
                    if (isAnagram(inputList.get(i), inputList.get(j))) {
                        AnagramArr.add(inputList.get(i));
                        AnagramArr.add(inputList.get(j));
                        inputList.remove(j--);
                    }
                }
            }
            // to count the anagram words
            int countAnagramWords =0;

            for (int p =0; p<AnagramArr.size();p++){
                if (AnagramArr.contains("")){
                    AnagramArr.remove("");
                }
            }
            for (int p =0; p<isP.size();p++){
                if (isP.contains("")){
                    isP.remove("");
                }
            }
            for (String st : AnagramArr){
//                System.out.print(st+", ");
                countAnagramWords++;
            }
            System.out.println("List of all anagrams: ");
            System.out.print(AnagramArr);
            System.out.println("\nList of palindrome words: ");
            System.out.print(isP);
            System.out.print("\nThe longest word in the file is: "+ longestWord(wordsArr));
            System.out.print("\nThe most repeated word in the file is: "+ Most_Repeated_word(wordsArr)[0]+", count: "+ Most_Repeated_word(wordsArr)[1] );

            try {
                int countSentences = sentencesCount(filename);
                System.out.print("\n"+countSentences+" sentences in this file");
            }catch (IOException ex){}
            System.out.printf("\nFile %s has\n%d characters\n%d words\n%d lines\n", filename, chars, words, lines);
            System.out.println("isPalindrome: "+count_isPal);
            System.out.println("isAnagrams: "+countAnagramWords );

        } catch (FileNotFoundException ex) {
            System.out.println("Such file doesn't exist: " + filename);
        }


    }
    // the longestWord method
    public static String longestWord(ArrayList<String > arr){
        int maxL = 0;
        String res = null;
        for (String str : arr) {
            if (str.length() > maxL) {
                maxL = str.length();
                res = str;
            }
        }
        return res;
    }
    public static boolean isPalindrome(String te){
        String reverse="";
        int r = te.length()-1;

        for (int i = r ; i>=0;i--){
            reverse = reverse+(te.charAt(i));
        }
        if (te.equals(reverse)){
            return true;
        }
        else{
            return false;
        }
    }
    public static boolean isAnagram(String string1, String string2) {
        if (string1.length() != string2.length()) {
            return false;
        }
        char[] a1 = string1.toCharArray();
        char[] a2 = string2.toCharArray();
        Arrays.sort(a1);
        Arrays.sort(a2);
        return Arrays.equals(a1, a2);
    }
    public static String[] Most_Repeated_word(ArrayList<String> arr){
        String[] res = new String[2];
        int f = 0;
        int t = 0;
        String MUW = null; // Mostly used word
        for (String word: arr) {
            t = 0;
            for (String w: arr) {
                if (word.equalsIgnoreCase(w)) {
                    t++;
                }
            }
            if (t >= f) {
                f = t;
                MUW = word;
            }
        }
        res[0] = MUW;
        res[1] = String.valueOf(f);
        return res;
    }
    public static int sentencesCount(String filename) throws IOException{
        BufferedReader c = new BufferedReader(new FileReader(filename));
        int sentenceCount=0;

        String st;

        String limit="?!.";
        int sentences = 0;
        while(c.ready())
        {
            st=c.readLine();
            sentenceCount=st.split("[!?.:]+").length;
            sentences+=sentenceCount;
        }
        return sentences;
    }
}
