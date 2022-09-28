/queue simple; 
:foreach i in=[find] \
do={  \
     :local sqName [get $i name]; \
     :local sqTotalBytes [get $i total-bytes]; \

     :local sqLevel [:find $sqName "[LevelA]"]; \
     :if ($sqLevel >= 0)  do={ \
        set $i limit-at=32000/32000 max-limit=64000/64000 burst-threshold=48000/48000 burst-limit=128000/128000 burst-time=30/30; \
        :if ($sqTotalBytes  > (100 * 1048576))  do={ \
          set $i limit-at=24000/24000 max-limit=32000/32000 burst-threshold=0/0 burst-limit=0/0 burst-time=0/0; \
        }; \
     } else {

       :set sqLevel [:find $sqName "[LevelB]"]; \
       :if ($sqLevel >= 0)  do={ \
           set $i limit-at=64000/64000 max-limit=128000/128000 burst-threshold=78000/78000 burst-limit=256000/256000 burst-time=30/30; \
           :if ($sqTotalBytes  > (200 * 1048576))  do={ \
             set $i limit-at=64000/64000 max-limit=64000/64000 burst-threshold=0/0 burst-limit=0/0 burst-time=0/0; \
           }; \

       } else { \

           :set sqLevel [:find $sqName "[LevelC]"]; \
           :if ($sqLevel >= 0)  do={ \
               set $i limit-at=72000/72000 max-limit=256000/256000 burst-threshold=96000/96000 burst-limit=1000000/1000000 burst-time=30/30; \
               :if ($sqTotalBytes  > (300 * 1048576))  do={ \
                  set $i limit-at=72000/72000 max-limit=72000/72000 burst-threshold=0/0 burst-limit=0/0 burst-time=0/0; \
                }; \
            }; \

        }; \
     }; \

     :if ($sqLevel >= 0) do { \
        :put ([get $i name] . " : " . [get $i limit-at] . " : " . [get $i max-limit]  . " : " . [get $i burst-limit]   . " : " . [get $i burst-threshold]  . " : " . [get $i burst-time]) ; \
     }; \

}
