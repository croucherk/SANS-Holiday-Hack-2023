# Ginger Breddie - Linux Refresher

The North Pole 🎁 Present Maker:
All the presents on this system have been stolen by trolls. Capture trolls by following instructions here and 🎁's will appear in the green bar below. Run the command "hintme" to receive a hint.

Type "yes" to begin:

## Prompts and Answers

1. Perform a directory listing of your home directory to find a troll and retrieve a present!

```bash
elf@feb5c2c28dd8:~$ ls | grep troll
troll_19315479765589239
```

2. Now find the troll inside the troll.

```bash
elf@feb5c2c28dd8:~$ cat troll_19315479765589239 
troll_24187022596776786
```

3. Great, now remove the troll in your home directory.

```bash
elf@feb5c2c28dd8:~$ rm troll_19315479765589239
```

4. Print the present working directory using a command.

```bash
elf@feb5c2c28dd8:~$ pwd
/home/elf
```

5. Good job but it looks like another troll hid itself in your home directory. Find the hidden troll!

```bash
elf@feb5c2c28dd8:~$ ls -a | grep troll
.troll_5074624024543078
```

6. Excellent, now find the troll in your command history.

```bash
elf@feb5c2c28dd8:~$ history | grep troll
    1  echo troll_9394554126440791
    2  ls | grep troll
    3  cat troll_19315479765589239 
    4  rm troll_19315479765589239 
    6  ls -a | grep troll
    7  history | grep troll
```

7. Find the troll in your environment variables.

```bash
elf@feb5c2c28dd8:~$ env | grep troll
z_TROLL=troll_20249649541603754
```

8. Next, head into the workshop.

```bash
elf@feb5c2c28dd8:~$ cd workshop/
```

9. A troll is hiding in one of the workshop toolboxes. Use "grep" while ignoring case to find which toolbox the troll is in.

```bash
elf@feb5c2c28dd8:~/workshop$ ls
electrical       toolbox_161.txt  toolbox_226.txt  toolbox_291.txt  toolbox_356.txt  toolbox_420.txt  toolbox_486.txt
present_engine   toolbox_162.txt  toolbox_227.txt  toolbox_292.txt  toolbox_357.txt  toolbox_421.txt  toolbox_487.txt
toolbox_0.txt    toolbox_163.txt  toolbox_228.txt  toolbox_293.txt  toolbox_358.txt  toolbox_422.txt  toolbox_488.txt
toolbox_1.txt    toolbox_164.txt  toolbox_229.txt  toolbox_294.txt  toolbox_359.txt  toolbox_423.txt  toolbox_489.txt
toolbox_10.txt   toolbox_165.txt  toolbox_23.txt   toolbox_295.txt  toolbox_36.txt   toolbox_424.txt  toolbox_49.txt
toolbox_100.txt  toolbox_166.txt  toolbox_230.txt  toolbox_296.txt  toolbox_360.txt  toolbox_425.txt  toolbox_490.txt
toolbox_101.txt  toolbox_167.txt  toolbox_231.txt  toolbox_297.txt  toolbox_361.txt  toolbox_426.txt  toolbox_491.txt
toolbox_102.txt  toolbox_168.txt  toolbox_232.txt  toolbox_298.txt  toolbox_362.txt  toolbox_427.txt  toolbox_492.txt
toolbox_103.txt  toolbox_169.txt  toolbox_233.txt  toolbox_299.txt  toolbox_363.txt  toolbox_428.txt  toolbox_493.txt
toolbox_104.txt  toolbox_17.txt   toolbox_234.txt  toolbox_3.txt    toolbox_364.txt  toolbox_429.txt  toolbox_494.txt
toolbox_105.txt  toolbox_170.txt  toolbox_235.txt  toolbox_30.txt   toolbox_365.txt  toolbox_43.txt   toolbox_495.txt
toolbox_106.txt  toolbox_171.txt  toolbox_236.txt  toolbox_300.txt  toolbox_366.txt  toolbox_430.txt  toolbox_496.txt
toolbox_107.txt  toolbox_172.txt  toolbox_237.txt  toolbox_301.txt  toolbox_367.txt  toolbox_431.txt  toolbox_497.txt
toolbox_108.txt  toolbox_173.txt  toolbox_238.txt  toolbox_302.txt  toolbox_368.txt  toolbox_432.txt  toolbox_498.txt
toolbox_109.txt  toolbox_174.txt  toolbox_239.txt  toolbox_303.txt  toolbox_369.txt  toolbox_433.txt  toolbox_499.txt
toolbox_11.txt   toolbox_175.txt  toolbox_24.txt   toolbox_304.txt  toolbox_37.txt   toolbox_434.txt  toolbox_5.txt
toolbox_110.txt  toolbox_176.txt  toolbox_240.txt  toolbox_305.txt  toolbox_370.txt  toolbox_435.txt  toolbox_50.txt
toolbox_111.txt  toolbox_177.txt  toolbox_241.txt  toolbox_306.txt  toolbox_371.txt  toolbox_436.txt  toolbox_500.txt
toolbox_112.txt  toolbox_178.txt  toolbox_242.txt  toolbox_307.txt  toolbox_372.txt  toolbox_437.txt  toolbox_51.txt
toolbox_113.txt  toolbox_179.txt  toolbox_243.txt  toolbox_308.txt  toolbox_373.txt  toolbox_438.txt  toolbox_52.txt
toolbox_114.txt  toolbox_18.txt   toolbox_244.txt  toolbox_309.txt  toolbox_374.txt  toolbox_439.txt  toolbox_53.txt
toolbox_115.txt  toolbox_180.txt  toolbox_245.txt  toolbox_31.txt   toolbox_375.txt  toolbox_44.txt   toolbox_54.txt
toolbox_116.txt  toolbox_181.txt  toolbox_246.txt  toolbox_310.txt  toolbox_376.txt  toolbox_440.txt  toolbox_55.txt
toolbox_117.txt  toolbox_182.txt  toolbox_247.txt  toolbox_311.txt  toolbox_377.txt  toolbox_441.txt  toolbox_56.txt
toolbox_118.txt  toolbox_183.txt  toolbox_248.txt  toolbox_312.txt  toolbox_378.txt  toolbox_442.txt  toolbox_57.txt
toolbox_119.txt  toolbox_184.txt  toolbox_249.txt  toolbox_313.txt  toolbox_379.txt  toolbox_443.txt  toolbox_58.txt
toolbox_12.txt   toolbox_185.txt  toolbox_25.txt   toolbox_314.txt  toolbox_38.txt   toolbox_444.txt  toolbox_59.txt
toolbox_120.txt  toolbox_186.txt  toolbox_250.txt  toolbox_315.txt  toolbox_380.txt  toolbox_445.txt  toolbox_6.txt
toolbox_121.txt  toolbox_187.txt  toolbox_251.txt  toolbox_316.txt  toolbox_381.txt  toolbox_446.txt  toolbox_60.txt
toolbox_122.txt  toolbox_188.txt  toolbox_252.txt  toolbox_317.txt  toolbox_382.txt  toolbox_447.txt  toolbox_61.txt
toolbox_123.txt  toolbox_189.txt  toolbox_253.txt  toolbox_318.txt  toolbox_383.txt  toolbox_448.txt  toolbox_62.txt
toolbox_124.txt  toolbox_19.txt   toolbox_254.txt  toolbox_319.txt  toolbox_384.txt  toolbox_449.txt  toolbox_63.txt
toolbox_125.txt  toolbox_190.txt  toolbox_255.txt  toolbox_32.txt   toolbox_385.txt  toolbox_45.txt   toolbox_64.txt
toolbox_126.txt  toolbox_191.txt  toolbox_256.txt  toolbox_320.txt  toolbox_386.txt  toolbox_450.txt  toolbox_65.txt
toolbox_127.txt  toolbox_192.txt  toolbox_257.txt  toolbox_321.txt  toolbox_387.txt  toolbox_451.txt  toolbox_66.txt
toolbox_128.txt  toolbox_193.txt  toolbox_258.txt  toolbox_322.txt  toolbox_388.txt  toolbox_452.txt  toolbox_67.txt
toolbox_129.txt  toolbox_194.txt  toolbox_259.txt  toolbox_323.txt  toolbox_389.txt  toolbox_453.txt  toolbox_68.txt
toolbox_13.txt   toolbox_195.txt  toolbox_26.txt   toolbox_324.txt  toolbox_39.txt   toolbox_454.txt  toolbox_69.txt
toolbox_130.txt  toolbox_196.txt  toolbox_260.txt  toolbox_325.txt  toolbox_390.txt  toolbox_455.txt  toolbox_7.txt
toolbox_131.txt  toolbox_197.txt  toolbox_261.txt  toolbox_326.txt  toolbox_391.txt  toolbox_456.txt  toolbox_70.txt
toolbox_132.txt  toolbox_198.txt  toolbox_262.txt  toolbox_327.txt  toolbox_392.txt  toolbox_457.txt  toolbox_71.txt
toolbox_133.txt  toolbox_199.txt  toolbox_263.txt  toolbox_328.txt  toolbox_393.txt  toolbox_458.txt  toolbox_72.txt
toolbox_134.txt  toolbox_2.txt    toolbox_264.txt  toolbox_329.txt  toolbox_394.txt  toolbox_459.txt  toolbox_73.txt
toolbox_135.txt  toolbox_20.txt   toolbox_265.txt  toolbox_33.txt   toolbox_395.txt  toolbox_46.txt   toolbox_74.txt
toolbox_136.txt  toolbox_200.txt  toolbox_266.txt  toolbox_330.txt  toolbox_396.txt  toolbox_460.txt  toolbox_75.txt
toolbox_137.txt  toolbox_201.txt  toolbox_267.txt  toolbox_331.txt  toolbox_397.txt  toolbox_461.txt  toolbox_76.txt
toolbox_138.txt  toolbox_202.txt  toolbox_268.txt  toolbox_332.txt  toolbox_398.txt  toolbox_462.txt  toolbox_77.txt
toolbox_139.txt  toolbox_203.txt  toolbox_269.txt  toolbox_333.txt  toolbox_399.txt  toolbox_463.txt  toolbox_78.txt
toolbox_14.txt   toolbox_204.txt  toolbox_27.txt   toolbox_334.txt  toolbox_4.txt    toolbox_464.txt  toolbox_79.txt
toolbox_140.txt  toolbox_205.txt  toolbox_270.txt  toolbox_335.txt  toolbox_40.txt   toolbox_465.txt  toolbox_8.txt
toolbox_141.txt  toolbox_206.txt  toolbox_271.txt  toolbox_336.txt  toolbox_400.txt  toolbox_466.txt  toolbox_80.txt
toolbox_142.txt  toolbox_207.txt  toolbox_272.txt  toolbox_337.txt  toolbox_401.txt  toolbox_467.txt  toolbox_81.txt
toolbox_143.txt  toolbox_208.txt  toolbox_273.txt  toolbox_338.txt  toolbox_402.txt  toolbox_468.txt  toolbox_82.txt
toolbox_144.txt  toolbox_209.txt  toolbox_274.txt  toolbox_339.txt  toolbox_403.txt  toolbox_469.txt  toolbox_83.txt
toolbox_145.txt  toolbox_21.txt   toolbox_275.txt  toolbox_34.txt   toolbox_404.txt  toolbox_47.txt   toolbox_84.txt
toolbox_146.txt  toolbox_210.txt  toolbox_276.txt  toolbox_340.txt  toolbox_405.txt  toolbox_470.txt  toolbox_85.txt
toolbox_147.txt  toolbox_211.txt  toolbox_277.txt  toolbox_341.txt  toolbox_406.txt  toolbox_471.txt  toolbox_86.txt
toolbox_148.txt  toolbox_212.txt  toolbox_278.txt  toolbox_342.txt  toolbox_407.txt  toolbox_472.txt  toolbox_87.txt
toolbox_149.txt  toolbox_213.txt  toolbox_279.txt  toolbox_343.txt  toolbox_408.txt  toolbox_473.txt  toolbox_88.txt
toolbox_15.txt   toolbox_214.txt  toolbox_28.txt   toolbox_344.txt  toolbox_409.txt  toolbox_474.txt  toolbox_89.txt
toolbox_150.txt  toolbox_215.txt  toolbox_280.txt  toolbox_345.txt  toolbox_41.txt   toolbox_475.txt  toolbox_9.txt
toolbox_151.txt  toolbox_216.txt  toolbox_281.txt  toolbox_346.txt  toolbox_410.txt  toolbox_476.txt  toolbox_90.txt
toolbox_152.txt  toolbox_217.txt  toolbox_282.txt  toolbox_347.txt  toolbox_411.txt  toolbox_477.txt  toolbox_91.txt
toolbox_153.txt  toolbox_218.txt  toolbox_283.txt  toolbox_348.txt  toolbox_412.txt  toolbox_478.txt  toolbox_92.txt
toolbox_154.txt  toolbox_219.txt  toolbox_284.txt  toolbox_349.txt  toolbox_413.txt  toolbox_479.txt  toolbox_93.txt
toolbox_155.txt  toolbox_22.txt   toolbox_285.txt  toolbox_35.txt   toolbox_414.txt  toolbox_48.txt   toolbox_94.txt
toolbox_156.txt  toolbox_220.txt  toolbox_286.txt  toolbox_350.txt  toolbox_415.txt  toolbox_480.txt  toolbox_95.txt
toolbox_157.txt  toolbox_221.txt  toolbox_287.txt  toolbox_351.txt  toolbox_416.txt  toolbox_481.txt  toolbox_96.txt
toolbox_158.txt  toolbox_222.txt  toolbox_288.txt  toolbox_352.txt  toolbox_417.txt  toolbox_482.txt  toolbox_97.txt
toolbox_159.txt  toolbox_223.txt  toolbox_289.txt  toolbox_353.txt  toolbox_418.txt  toolbox_483.txt  toolbox_98.txt
toolbox_16.txt   toolbox_224.txt  toolbox_29.txt   toolbox_354.txt  toolbox_419.txt  toolbox_484.txt  toolbox_99.txt
toolbox_160.txt  toolbox_225.txt  toolbox_290.txt  toolbox_355.txt  toolbox_42.txt   toolbox_485.txt

elf@feb5c2c28dd8:~/workshop$ cat *.txt | grep -i troll
tRoLl.4056180441832623
```

10. A troll is blocking the present_engine from starting. Run the present_engine binary to retrieve this troll.

```bash
elf@feb5c2c28dd8:~/workshop$ ls -l present_engine 
-r--r--r-- 1 elf elf 4990336 Dec  2 22:19 present_engine
elf@feb5c2c28dd8:~/workshop$ chmod +x present_engine 
elf@feb5c2c28dd8:~/workshop$ ./present_engine 
troll.898906189498077
```

11. Trolls have blown the fuses in /home/elf/workshop/electrical. cd into electrical and rename blown_fuse0 to fuse0.

```bash
elf@feb5c2c28dd8:~/workshop$ cd /home/elf/workshop/electrical/
elf@feb5c2c28dd8:~/workshop/electrical$ mv blown_fuse0 fuse0
```

12. Now, make a symbolic link (symlink) named fuse1 that points to fuse0

```bash
elf@feb5c2c28dd8:~/workshop/electrical$ ln -s fuse0 fuse1
```

13. Make a copy of fuse1 named fuse2.

```bash
elf@feb5c2c28dd8:~/workshop/electrical$ cp fuse1 fuse2
```

14. We need to make sure trolls don't come back. Add the characters "TROLL_REPELLENT" into the file fuse2.

```bash
elf@feb5c2c28dd8:~/workshop/electrical$ echo TROLL_REPELLENT >> fuse2
```

15. Find the troll somewhere in /opt/troll_den.

```bash
elf@feb5c2c28dd8:/opt/troll_den$ find . -iname "*troll*"
./plugins/embeddedjsp/src/main/java/org/apache/struts2/jasper/compiler/ParserController.java
./apps/showcase/src/main/resources/tRoLl.6253159819943018
./apps/rest-showcase/src/main/java/org/demo/rest/example/IndexController.java
./apps/rest-showcase/src/main/java/org/demo/rest/example/OrdersController.java
elf@feb5c2c28dd8:/opt/troll_den$ cat apps/showcase/src/main/resources/tRoLl.6253159819943018
```

16. Find the file somewhere in /opt/troll_den that is owned by the user troll.

```bash
elf@feb5c2c28dd8:/opt/troll_den$ find . -user troll
./apps/showcase/src/main/resources/template/ajaxErrorContainers/tr0LL_9528909612014411
```

17. Find the file created by trolls that is greater than 108 kilobytes and less than 110 kilobytes located somewhere in /opt/troll_den.

```bash
elf@feb5c2c28dd8:/opt/troll_den$ find . -size +108k -size -110k
./plugins/portlet-mocks/src/test/java/org/apache/t_r_o_l_l_2579728047101724
```

18. List running processes to find another troll.

```bash
elf@feb5c2c28dd8:/opt/troll_den$ ps aux
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
init           1  0.0  0.0  20112 16520 pts/0    Ss+  18:20   0:00 /usr/bin/python3 /usr/local/bin/tmuxp load ./mysessio
elf         8101  0.3  0.0  31520 26816 pts/2    S+   18:33   0:00 /usr/bin/python3 /14516_troll
elf         8477  0.0  0.0   7672  3164 pts/3    R+   18:34   0:00 ps aux
```

19. The 14516_troll process is listening on a TCP port. Use a command to have the only listening port display to the screen.

```bash
elf@feb5c2c28dd8:/opt/troll_den$ netstat -tln
Active Internet connections (only servers)
Proto Recv-Q Send-Q Local Address           Foreign Address         State      
tcp        0      0 0.0.0.0:54321           0.0.0.0:*               LISTEN
```

20. The service listening on port 54321 is an HTTP server. Interact with this server to retrieve the last troll.

```bash
elf@feb5c2c28dd8:/opt/troll_den$ curl http://127.0.0.1:54321
troll.73180338045875
```

21. Your final task is to stop the 14516_troll process to collect the remaining presents.

```bash
elf@feb5c2c28dd8:/opt/troll_den$ ps aux | grep 14516_troll
elf         8101  0.1  0.0 105616 27484 pts/2    S+   18:33   0:00 /usr/bin/python3 /14516_troll
elf         9481  0.0  0.0   5220   732 pts/3    S+   18:35   0:00 grep --color=auto 14516_troll
elf@feb5c2c28dd8:/opt/troll_den$ kill 8101
```

22. Congratulations, you caught all the trolls and retrieved all the presents! Type "exit" to close...

```bash
elf@feb5c2c28dd8:/opt/troll_den$ exit
```

