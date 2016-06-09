# Promises - The Future is bright ( resolve, reject )

But now my code is a pyramid of doom!

    function add(v1, v2, cb){
        setTimeout(function(){
            cb(v1 + v2);
        }, 0);
    }

    add(1, 1, function(result){
        add(result, 2, function(result2){
            console.log('result:', result2);
        });
    });

Well Have I got the trick for you!

    first what is a promise?
    Promise is a construct that lets you 'defer' callbacks using an object to allow for chaining


    function add(v1, v2){
        var result = new Promise(function(result, reject){
            setTimeout(function(){
                result(v1 + v2);
            }, 0);
        });
        return result;
    }

How the newbs of the internet show you ( DON'T BE THAT GUY ) !

    add(1, 1).then(function(result){
        add(result, 2).then(function(result2){
            console.log('result:', result2);
        });
    });

Your code is still messy, and hard to read, and you should notice your doing something wrong...
Instead of nesting your promises and function calls, return any promise you get to the parent scope!!!
Well that was easy:

    add(1, 1).then(function(result){
      return add(result, 2);
    }).then(function(result2){
      console.log('result:', result2);
    });


Now your ready for Q : [Lets Learn Q](Q.md)