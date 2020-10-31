# DSA


public static void SCC(){

    //Topological Order

    ArrayList<Integer> path = new ArrayList<>();
    boolean [] vis = new boolean[N];
    for(int i=0;i<N;i++){
        if(!vis[i]) DFS_SSC(i,vis,path);
    }

    //Reverse graph

    ArrayList<Integer> [] ngraph = new ArrayList<>();
    for(int i=0;i<N;i++) ngraph[i] = new ArrayList<>();

    for(int i=0;i<N;i++){
        for(int e:graph[i]){
            ngraph[e].add(i);
        }
    }

    //DFS over topological Order
    vis = new boolean[N];

    int count =0;

    for(int i=path.size()-1;i>=0;i--){
        if(!vis[path.get(i)]){
            count++;
            DFS_SSC2(path.get(i),ngraph,vis);
        }
    }
}

public static int findPath(int [][] dp , int sr , int sc , String path){

    if(sr == dp.length -1 && sc == dp[0].length-1){
        System.out.println(path);
        return 1;
    }
 
 
     int count = 0;
 for(int d=0;d<dir.length;d++){
     for(int i=1;i<4;i++){
     int x = sr + i*dir[d][0];
     int y = sc + i*dir[d][1];
     
     if(x>=0 && y >=0 && x <dp.length && y <dp[0].length){
         count+=findPath(dp,x,y,path+psf[d]+i);
     }
 }
}
    return count;
 }
 



