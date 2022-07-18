# Stream Tags  
(링크: https://wiki.gnuradio.org/index.php?title=Stream_Tags)  

GNU Radio는 블록 간에 데이터를 전송하기 위해, Massage Passing이라는 메커니즘을 사용함.  
Massage Passing은 어떤 블록에서 데이터에 메시지를 부여하고, 다른 블록에서 읽는 방식으로 메시지를 전달하는 메커니즘임.  
Massage Passing의 큰 단점으로는 비동기화가 있음. 데이터 스트림의 순서대로 메시지가 도착하지 않을 수 있다는 것임.  
이 문제점을 해결하기 위해 데이터 스트림에 tag를 부여함. 데이터를 수신한 후, tag 값으로 데이터를 정렬하면  

Stream tag는 블록의 work 함수에 의해 생성되고 다른 블록에 의해 전송이 중단되거나, sink 블록에 도달할 때까지 해당 tag가 부여된 개별적인 sample 옆에서 같이 흐름.  
Stream tag는 데이터 스트림 내의 특정한 항목을 위해 정의되고 key:value 쌍의 형태임.  

데이터 스트림 모델에서, 각각의 블록의 work 함수에 0부터 N-1까지 참조할 수 있는 데이터 스트림을 담는 버퍼가 주어짐.  
버퍼의 0,1,...,N-1은 데이터 스트림안에서의 상대적인 위치(offset)을 의미함.  
절대적인 참조 값은 flowgraph의 시작부터(0) 아이템 당 1씩 계속 증가함.  

nitems_read(unsigned int which_input) 함수를 통해서 input으로 들어오는 데이터 스트림의 '읽은(지나간) 아이템들의 개수' 즉, 현재 들어오는 아이템의 참조 위치 값을 구할 수 있음.  
