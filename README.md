# SystemPRO
시스템 프로그래밍 명령어

1.디렉터리 생성
2.디렉터리 이용
3.파일 크기가 0인 파일 생성
4.파일 권한 변경
5.파일(디렉터리)삭제


                    TEST
        (d)a01    (-)b01     (d)c
        (d)a02            (-)history
        (d)a03            (-)history_30313
       

                 
                 
       history>c/history //c디렉터리 안에 history 파일에 기록저장
       touch b01 //파일 값이 0인 파일 생성
       
       
       :w history_30313 //history원본 파일을 다른이름으로 저장가능
       :q! //나가기
       <권한 변경>
       chmod -숫자 chmod (권한 2진수 숫자) (파일명)
            
       읽기 권한 있으면 1,없으면 0
       (RWX) 읽,쓰,실
       
       <파일 디렉터리로 삭제>.
       rm -r a01/a02
       
