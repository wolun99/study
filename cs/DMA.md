### DMA(직접 메모리 접근)

- 고성능이라는 말이 따라다님
- cpu 에서 RAM으로 예약하고 RAM 내부에서 복사할 경우도 있고 Device의 영역으로 가서 실행됨 중간에 인터럽트가 발생되기 때문에 중간중간 실행이 중지됨(DMA를 적용하지 않았을 때)
- 특정 하드웨어의 하위 시스템이 직접적으로 메모리와 접근하게 하는 기능
- 네트워크 데이터 i/o buffer에전달 socket에 전달해서 segment 해서 네트워크에 전달
- 중간 단계를 없애고 바로 device로 데이터를 전달할 수 있다.
- 운영체제가 kernel을 제어하고 user 영역의 부분을 제외하고 실행가능하게 해줌
- RAM의 일부분을 device에게 할당해서 성능이 매우 좋아짐
- 가상환경에 적용하게 되면 성능이 어마어마하게 좋아짐
