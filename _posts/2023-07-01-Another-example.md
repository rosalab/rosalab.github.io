---
title: Another example
layout: post
---


This post has no description and header image. 

Long Text : Morbi efficitur magna turpis, tincidunt tristique sapien eleifend a. Mauris sit amet finibus quam, in condimentum elit. Nunc dignissim consequat tincidunt. Etiam ultrices orci non molestie fringilla. Maecenas mi diam, luctus vel risus quis, porta gravida nisl. Curabitur auctor placerat orci at convallis. Nulla ultrices facilisis iaculis. Integer eget enim in felis scelerisque ultrices. Nulla gravida erat ac eros faucibus consequat. Donec tempus ultrices dolor, non mattis lorem posuere vitae. Curabitur sollicitudin nec velit a imperdiet. Nulla quis quam eget augue elementum congue eget id velit. Integer euismod consectetur dui eu iaculis. Aliquam ut lobortis purus. Aliquam malesuada accumsan felis, id tincidunt ipsum. 


Sample code block :

{% highlight C++ %}
int main(){                                                              
                                                                         
        srand(time(0));                                                  
        unique_ptr<Line> l1;                                             
        unique_ptr<Line> l2;                                             
                                                                         
        int r = rand()%2;                                                
        if(r==0){                                                        
                l1 = make_unique<Line>(1);                               
                l2 = make_unique<Line>(2);                               
        }                                                                
        else{                                                            
                                                                         
                l1 = make_unique<Line>(1);                               
        }                                                                
                                                                         
        throw -1;                                                        
                                                                         
        if(r==1){                                                        
                l1.reset();                                              
        }                                                                
        else{                                                            
                l1.reset();                                              
                l2.reset();                                              
        }                                                                
                                                                         
        cout<<"Ending..\n";                                              
        return 0;                                                        
}                                                                        
{% endhighlight %}
