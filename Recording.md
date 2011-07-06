Say you have the following inst:

    (definst bong [note 60 velocity 0.5 attack 0.01 decay 1] 
      (let [freq (midicps note) 
            src (+ (sin-osc freq) 
                   (* 0.5 (sin-osc (* 2.1 freq))) 
                   (* 0.4 (sin-osc (* 4.9 freq))) 
                   (* 0.3 (sin-osc (* 7.1 freq))) 
                   (* 0.2 (sin-osc (* 8.9 freq))) 
                   (* 0.1 (triangle (* 11.1 freq))) 
                   (* 0.1 (triangle (* 2.4 freq))) 
                   (* 0.1 (square (* 1.3 freq))) 
                   (* 0.1 (triangle (* 2.8 freq))) 
                   (* 0.1 (square (* 4.2 freq)))) 
            env (env-gen (perc attack decay) :action :free)] 
        (* velocity src env))) 

and you wish to create a wav file containing a recording of it playing. Here's how you do it...

First create a buffer to store your recording - this is in samples, so 44100 will record 1s of audio at the standard rate: 

    (def b (buffer 44100)) 

and then modifying the inst to output to buffer b using the record-buf ugen:

    (definst bong [note 60 velocity 0.5 attack 0.01 decay 1] 
      (let [freq (midicps note) 
            src (+ (sin-osc freq) 
                   (* 0.5 (sin-osc (* 2.1 freq))) 
                   (* 0.4 (sin-osc (* 4.9 freq))) 
                   (* 0.3 (sin-osc (* 7.1 freq))) 
                   (* 0.2 (sin-osc (* 8.9 freq))) 
                   (* 0.1 (triangle (* 11.1 freq))) 
                   (* 0.1 (triangle (* 2.4 freq))) 
                   (* 0.1 (square (* 1.3 freq))) 
                   (* 0.1 (triangle (* 2.8 freq))) 
                   (* 0.1 (square (* 4.2 freq)))) 
            env (env-gen (perc attack decay) :action :free)] 
        (record-buf (* velocity src env) b :action  2 :loop 0))) 

Trigger the inst: 
    (bong) 
and then issued a buffer-save command to save to a file called "bong.wav" in the directory of the current project: 
    (buffer-save b "bong.wav" ) 

your file should be in the root directory of your project for your listening pleasure :-)