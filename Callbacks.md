# Callbacks - What are they and how do they work?

# First Why - Async?

    Classic Code Practices from Java/C land say I should write code like

    function add(v1, v2){
        return v1 + v2;
    }

    var result = add(1, 1);
    console.log('result:', result);

    //do some other stuff

    result = add(result, 2);
    console.log('result:', result);

Expected Result:

        result: 2
        //other stuff
        result: 4

But whats the problem with this?

    add() is blocking so your other stuff has to wait on add even if it does not depend on it


But callbacks how?

        function add(v1, v2, cb){
            cb(v1 + v2);
        }

        add(1, 1, function(result){
            console.log('result:', result);
        });

Expected Result:

        result: 2

But that doesnt save us anything
    Yes, not yet


    function add(v1, v2, cb){
        setTimeout(function(){
            cb(v1 + v2);
        }, 0);
    }

    add(1, 1, function(result){
        console.log('result:', result);
    });

Expected Result:

            result: 2

Now because of the setTimeout our code is Asynchronous and not blocking
    Note: you should use process.nextTick() in NodeJS not setTimeout


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

Now your Ready for : [Lets Learn Promises](Promises.md)