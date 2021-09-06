<!-- # PS -->
<!-- Priority scheduling non primitive algorithm -->

import java.util.*;
import java.io.*;

class PriorityScheduling{
    // utiltiy function to get a process 
    // that is not visited 
    // and available to execute



    // ArrayList    A contains all the processes that are available to execute
    // HashMap      H contains the processes as keys and a string value as the 
    //              startingtime  duration priority

    public String GET(ArrayList<String> A,HashMap<String,String> H){

        // checking priority of all the 
        // priocesses that are available 
        // to exeute


        // List to store all the processes
        // based on priority

        // only processes with highest priority
        // are stored 
        ArrayList<String> Prior=new ArrayList<String>();

        // initialize maxPriority to min value
        int maxPrior=Integer.MIN_VALUE;

        // loop to check for the priorities of 
        // all the available processes
        // and find max priority
        for(int i=0;i<A.size();i++){
            // find string a string that contains 
            // the startingtime , duration and priority
            // as a string seperated by a space : " ";
            String find=H.get(A.get(i));
            String Arr[]=find.split(" ");
            // Priority is the third value of string
            String P=Arr[2];
            // converting int to string
            int pi=Integer.parseInt(P);

            if(maxPrior<pi) maxPrior=pi;        
        }

        // loop to add all the processes with highest priority 
        // to Prior arraylist
        for(int i=0;i<A.size();i++){
            String find=H.get(A.get(i));
            String Arr[]=find.split(" ");
            String P=Arr[2];
            int pi=Integer.parseInt(P);
            if(maxPrior==pi) Prior.add(A.get(i));
        }

        // if prior size is 1 return that value
        if(Prior.size()==1) return Prior.get(0);

        // else check for the processes having 
        // least starting time and max priority


        // ArrayList to store the processes that 
        // have the least starting time

        ArrayList<String> LeastStartingTime=new ArrayList<String>();

        // est to get the least starting time
        int est=Integer.MAX_VALUE;


        // loop to check for the starting time of 
        // all the available processes with max proirity
        // and find least starting time

        for(int i=0;i<Prior.size();i++){

            // find string a string that contains 
            // the startingtime , duration and priority
            // as a string seperated by a space : " ";

            String find=H.get(Prior.get(i));

            String Arr[]=find.split(" ");
            // getting the starting time for the process

            String S=Arr[0];
            // conveting the string value to int 
            int est2=Integer.parseInt(S);
            if(est>est2) est=est2;
        }

        // loop to add all the processes with least starting time 
        // to LeastStartingTime arraylist

        for(int i=0;i<Prior.size();i++){
            String find=H.get(Prior.get(i));
            String Arr[]=find.split(" ");
            String S=Arr[0];
            int est2=Integer.parseInt(S);
            if(est==est2) LeastStartingTime.add(Prior.get(i));
        }
        
        // if LeastStartingTime contains only 1 process
        // return it because it will be the process with highest
        // priority and least starting time 
        if(LeastStartingTime.size()==1) return LeastStartingTime.get(0);

        // else find the processes with the lowest duration 

        // Arraylist to store the processes with lowest duration 
        ArrayList<String> LD=new ArrayList<String>();

        // int variable ld to store the lowest duration process
        // from the proceeses that are present in LeastStartingTime
        // List 
        int ld=Integer.MAX_VALUE;

        for(int i=0;i<LeastStartingTime.size();i++){

            // find string a string that contains 
            // the startingtime , duration and priority
            // as a string seperated by a space : " ";

            String find=H.get(Prior.get(i));
            String Arr[]=find.split(" ");
            String D=Arr[1];
            int est2=Integer.parseInt(D);
            if(ld>est2) ld=est2;
        }

        for(int i=0;i<LeastStartingTime.size();i++){

            String find=H.get(Prior.get(i));
            String Arr[]=find.split(" ");

            // String D for the duration of the process
            String D=Arr[1];
            int est2=Integer.parseInt(D);
            if(ld==est2) LD.add(LeastStartingTime.get(i));
        }
        // Now we have a list LD that contains all the processes that are 
        // available to execute, and have higest priorites and least 
        // arrival time and shortest duration
        // If it contains more than one process
        // return with least index
        return LD.get(0);
    }


    // utility function to find 
    // the order of execution of processes

    // s[] = arrival time of processes [1,2,3...N]
    // d[] = duration time of processes [1,2,3...N]
    // p[] = priorities of processes [1,2,3...N]
    
    public int[] taskRunner(int[] s, int[] d, int[] p) {

        // Map that would contain the process as key 
        // and arrival time, duration time and priority as value
        // Map < Process, "s[Process] d[Process] p[Process]" >
        // Key = Process
        // Value = "s[Process] d[Process] p[Process]" 
        // Value as string 
        HashMap<String,String> H=new HashMap<String,String>();


        // n is total no. of processes 
        int n=s.length;


        // Initalize currTime to zero
        int currTime=0;

        // loop to store all the key value pairs
        for(int i=0;i<n;i++){
            String process="P"+i;
            String sdp=s[i]+" "+d[i]+" "+p[i];
            H.put(process,sdp);   
        }


        // Output array Out[] for the order 
        // of execution
        int Out[]=new int[n];
        ArrayList<String> OutPut=new ArrayList<String>();


        // HashSet for checking whether a process is executed 
        // already or not
        HashSet<String> visited=new HashSet<String>();


        // Available to run processes are stored in arraylist
        ArrayList<String> AvailableToRun=new ArrayList<String>();


        // loop to find the processes that are available 
        // for execting that have starting time less than the 
        // current time
        for(int i=0;i<n;i++){
            String process="P"+i;
            if(s[i]<=currTime) AvailableToRun.add(process);
        }

        // if we are unable to find any such
        // than increase the currTime as 
        // no processes were availble to execute

        if(AvailableToRun.size()==0){

            int minTime1=Integer.MAX_VALUE;
            // finding the minimum starting time 
            // for a process that is grater than the current time 
            // and the process is not executed
            for(int i=0;i<n;i++){
                String process="P"+i;
                if(s[i]<=currTime && !visited.contains(process) && !AvailableToRun.contains(process)) AvailableToRun.add(process);
                if(!visited.contains(process)){
                    if(minTime1>s[i]) minTime1=s[i];
                }
            }
            if(AvailableToRun.size()==0){
                for(int i=0;i<n;i++){
                    String process="P"+i;
                    if(s[i]==minTime1 && !AvailableToRun.contains(process)) AvailableToRun.add(process);
                }   
                currTime=minTime1;
            }
        }

        // ininalize a variable to n 
        // to stop the loop 
        // after all the procees that are exectuted

        int ctr=n;
        while(ctr>=0){

            if(ctr==0) break;

            // if only 1 process is available to execute
            // and is not executed yet execute it

            if(AvailableToRun.size()==1 && !visited.contains(AvailableToRun.get(0))){

                // String processExecuted for the process that would be executed
                String processExecuted=AvailableToRun.get(0);

                // find string to get the value associated with that process
                String find=H.get(processExecuted);
                String Arr[]=find.split(" ");
                String D=Arr[1];
                
                // find the duration of the process 
                // to be executed 
                // and increment the current Time by duration of 
                // process
                int di=Integer.parseInt(D);
                currTime+=di;

                // add the process to output
                OutPut.add(processExecuted);

                // mark the proceess visited
                visited.add(processExecuted);

                // remove the process that is executed 
                // so reduce time in calculting the processes 
                // that are avilable and not exectued
                AvailableToRun.remove(processExecuted);
                ctr--;
                if(ctr==-1) break;
            }
            else{
                if(ctr==-1) break;
                // use the utility function to find 
                // process to be executed
                String processTobeExecuted=GET(AvailableToRun,H);

                // mark it visited 
                visited.add(processTobeExecuted);

                // getting duration time to increment current Time
                String find=H.get(processTobeExecuted);
                String Arr[]=find.split(" ");
                String D=Arr[1];
                int di=Integer.parseInt(D);
                currTime+=di;

                // add it to output
                OutPut.add(processTobeExecuted);
                visited.add(processTobeExecuted);
                AvailableToRun.remove(processTobeExecuted);
                ctr--;
                if(ctr==0) break;
            }


            // now find the next availble process to execute

            int minTime=Integer.MAX_VALUE;
            for(int i=0;i<n;i++){
                String process="P"+i;
                if(s[i]<=currTime && !visited.contains(process) && !AvailableToRun.contains(process)) AvailableToRun.add(process);
                if(!visited.contains(process)){
                    if(minTime>s[i]) minTime=s[i];
                }
            }

            // if we are unable to find any such
            // than increase the currTime as 
            // no processes were availble to execute

            
            if(AvailableToRun.size()==0){
                for(int i=0;i<n;i++){
                    String process="P"+i;
                    if(s[i]==minTime && !AvailableToRun.contains(process)) AvailableToRun.add(process);
                }   
                currTime=minTime;
            }
        }

        // finally copying data from Output to Out

        for(int i=0;i<n;i++){
            String process=OutPut.get(i);
            char d1[]=new char[process.length()-1];
            for(int i1=0;i1<d1.length;i1++) d1[i1]=process.charAt(i1+1);
            String ans=new String(d1);
            int ret=Integer.parseInt(ans);
            Out[i]=ret;
        }

        return Out;
    }
}


class Driver{
    public static void main(String[] args) {
        Scanner s=new Scanner(System.in);
        int n=s.nextInt();
        int s1[]=new int[n];
        int d[]=new int[n];
        int p[]=new int[n];
        PriorityScheduling obj=new PriorityScheduling();
        for(int i=0;i<n;i++) s1[i]=s.nextInt();
        for(int i=0;i<n;i++) d[i]=s.nextInt();
        for(int i=0;i<n;i++) p[i]=s.nextInt();
        int ans[]=obj.taskRunner(s1,d,p);
        System.out.println(Arrays.toString(ans));
    }
}
