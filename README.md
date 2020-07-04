# utl-another-classic-long-to-wide-transpose-using-Arts-untanspose-macro
Another classic long to wide transpose using Arts untanspose macro   
    classic long to wide transpose using Arts untanspose macro                                                                  
                                                                                                                                
    * AUTHORS: Arthur Tabachneck, Gerhard Svolba, Joe Matise and Matt Kastin                                                    
      art297@rogers.com                                                                                                         
                                                                                                                                
      github                                                                                                                    
      https://tinyurl.com/y9omsf4q                                                                                              
      https://github.com/rogerjdeangelis/utl-another-classic-long-to-wide-transpose-using-Arts-untanspose-macro                 
                                                                                                                                
       Method                                                                                                                   
       ======                                                                                                                   
                                                                                                                                
          "Untransposes wider SAS datasets back to either the less wide                                                         
           state that existed before the file was transposed, or to a long file"                                                
                                                                                                                                
           Works well with wide tables where variables have systematic suffixes                                                 
           You can even have mutiple sets of variables (x1 x2 x3   y1 y2 y3)                                                    
                                                                                                                                
              stem1 stem2 stem3                                                                                                 
              stem1_1 stem1_2 stem2_1 stem2_2 stem3_3                                                                           
              stem_a stem_b stem_c                                                                                              
                                                                                                                                
    This is a usefull tool. Simple and fast.                                                                                    
                                                                                                                                
    https://communities.sas.com/t5/SAS-Programming/Wide-to-Long/m-p/666400                                                      
                                                                                                                                
    related repos                                                                                                               
    https://tinyurl.com/y6wldxtr                                                                                                
    https://github.com/rogerjdeangelis?tab=repositories&q=untranspose+in%3Areadme&type=&language=                               
                                                                                                                                
    macros (also available from Art)                                                                                            
    https://tinyurl.com/y9nfugth                                                                                                
    https://github.com/rogerjdeangelis/utl-macros-used-in-many-of-rogerjdeangelis-repositories                                  
                         _                                                                                                      
    (_)_ __  _ __  _   _| |_                                                                                                    
    | | `_ \| `_ \| | | | __|                                                                                                   
    | | | | | |_) | |_| | |_                                                                                                    
    |_|_| |_| .__/ \__,_|\__|                                                                                                   
            |_|                                                                                                                 
                                                                                                                                
    WORK.HAVE total obs=2                                                                                                       
                                                                                                                                
                                        Measure array                          Time array                                       
                          ===============================================   ==================                                  
     ID  APPROACH DIET    MES1_1  MES1_2  MES1_3  MES2_1   MES2_2  MES2_3   TIME1 TIME2  TIME3                                  
                                                                                                                                
      1      1      1        5      10      103   water    water   water      10    85    100                                   
      2      2      2        5      11      103   protein  water   water      12    92    102                                   
                 _               _                                                                                              
      ___  _   _| |_ _ __  _   _| |_                                                                                            
     / _ \| | | | __| `_ \| | | | __|                                                                                           
    | (_) | |_| | |_| |_) | |_| | |_                                                                                            
     \___/ \__,_|\__| .__/ \__,_|\__|                                                                                           
                    |_|                                                                                                         
                                                                                                                                
    Up to 40 obs WORK.WANT total obs=6                                                                                          
                                                                                                                                
                                                                                                                                
                                   Variables   Suffix     Suffix    Suffix                                                      
                                    suffix     Removed    Removed   Removed                                                     
                                                                                                                                
      ID    APPROACH    DIET        SUFX        TIME       MES1_     MES2_                                                      
                                                                                                                                
       1        1         1           1           10          5     water                                                       
       1        1         1           2           85         10     water                                                       
       1        1         1           3          100        103     water                                                       
                                                                                                                                
       2        2         2           1           12          5     protein                                                     
       2        2         2           2           92         11     water                                                       
       2        2         2           3          102        103     water                                                       
                                                                                                                                
     _ __  _ __ ___   ___ ___  ___ ___                                                                                          
    | `_ \| `__/ _ \ / __/ _ \/ __/ __|                                                                                         
    | |_) | | | (_) | (_|  __/\__ \__ \                                                                                         
    | .__/|_|  \___/ \___\___||___/___/                                                                                         
    |_|                                                                                                                         
                                                                                                                                
    %untranspose(data=have, out=want, by=id approach diet,id=sufx, var=time mes1_ mes2_)                                        
                                                                                                                                
      ___ ___   __| | ___    __ _  ___ _ __                                                                                     
     / __/ _ \ / _` |/ _ \  / _` |/ _ \ `_ \                                                                                    
    | (_| (_) | (_| |  __/ | (_| |  __/ | | |                                                                                   
     \___\___/ \__,_|\___|  \__, |\___|_| |_|                                                                                   
                            |___/                                                                                               
                                                                                                                                
    data work.want                                                                                                              
    ( keep=id approach diet sufx time mes1_ mes2_ );                                                                            
    set work.have;                                                                                                              
    informat sufx 8. ;                                                                                                          
    format sufx 8. ;                                                                                                            
    length TIME 8 ;                                                                                                             
    TIME=TIME1;                                                                                                                 
    length MES1_ 8 ;                                                                                                            
    MES1_=MES1_1;                                                                                                               
    length MES2_ $ 8 ;                                                                                                          
    MES2_=MES2_1;                                                                                                               
    if (not missing(MES2_)) or (not missing(MES1_)) or (not missing(TIME)) then do;                                             
    sufx=1;                                                                                                                     
    output;                                                                                                                     
    end;                                                                                                                        
    TIME=TIME2;                                                                                                                 
    MES1_=MES1_2;                                                                                                               
    MES2_=MES2_2;                                                                                                               
    if (not missing(MES2_)) or (not missing(MES1_)) or (not missing(TIME)) then do;                                             
    sufx=2;                                                                                                                     
    output;                                                                                                                     
    end;                                                                                                                        
    TIME=TIME3;                                                                                                                 
    MES1_=MES1_3;                                                                                                               
    MES2_=MES2_3;                                                                                                               
    if (not missing(MES2_)) or (not missing(MES1_)) or (not missing(TIME)) then do;                                             
    sufx=3;                                                                                                                     
    output;                                                                                                                     
    end;                                                                                                                        
    run;                                                                                                                        
    */                                                                                                                          
                                                                                                                                
                                                                                                                                
