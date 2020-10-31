# DSA


public static int boardPathDP(int sp, int ep , int [] dp){
    for(sp = ep;sp>=0;sp--){
        if(sp == ep){
            dp[sp] = 1;
            continue;
        }


        for(int dice =1 ;dice<=6 && sp + dice  <=ep;dice++){
            dp[sp]+=dp[sp+dice];
        }
    }

    return dp[0];
}

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
 
 
 
public static int Friendspairing(int n, int [] dp)
{
    int c = (int)1e9 + 7;
    for(int n=0;n<=N;n++){
        if(n<=1)
        {
            dp[n] = 1;
            continue;
        }

        dp[n] = (dp[n-1]%c + (dp[n-2] %c *(n-1)%c)%c)%c;
    }

    return dp[N];
}


public static int boardPathOpti(int n)
{
    LinkedList<Integer> ll = new LinkedList<>();

    for(int si =n;si>=0;si--)
    {
        if(ll.size()<=1) ll.addFirst(1);
        else if(ll.size()<=6) ll.addLast(2 * ll.getFirst());
        else{
            ll.addLast(2 * ll.getFirst() - ll.getLast());
        }
    }

    return ll.getFirst();
}

 public static void bellmanFordAlgo(int[][] edges,int N,int src){
        int[] dis = new int[N];
        Arrays.fill(dis,(int)1e8);
        dis[src] = 0;
        boolean negativeCycle = false;

        for(int i=1;i <= N;i++){
            
            boolean isAnyUpdate = false;
            
            int[] ndis = new int[N];
            for(int i=0;i<N;i++) ndis[i] = dis[i];

            for(int[] e : edges){
                if(dis[e[0]]!= (int)1e8 && dis[e[0]] + e[2] < ndis[e[1]]){
                    ndis[e[1]] = dis[e[0]] + e[2];
                    isAnyUpdate = true;
                }
            }

            dis = ndis;


            if(isAnyUpdate && i == N) negativeCycle = true;
            if(!isAnyUpdate && i < N) break;
        }
    }



public static void DijkstraAlgo(ArrayList<Edge>[] graph,int N){
        boolean[] vis = new boolean[N];
        int[] dis = new int[N];
        int[] par = new int[N];

        Arrays.fill(dis,(int)1e8);
        Arrays.fill(par,-1)

        PriorityQueue<dijkstraPair> que = new PriorityQueue<>((a,b)->{
            return a.wsf - b.wsf; // this - other
        });

        que.add(new dijkstraPair(0,-1,0));
        dis[0] = 0;

        int EdgesCount = 1;
        while(EdgesCount <= N - 1){
            dijkstraPair pair = que.remove();
            
            if(vis[pair.vtx]) continue;
            if(pair.par != -1) EdgesCount++;

            vis[pair.vtx] = true;
            par[pair.vtx] = pair.par;

            for(Edge e: graph[pair.vtx]){
                if(!vis[e.v] && pair.wsf + e.w < dis[e.v]){
                    dis[e.v] = pair.wsf + e.w;
                    que.add(new primsPair(e.v,pair.vtx,pair.wsf + e.w));
                }
            }
        }
    }


