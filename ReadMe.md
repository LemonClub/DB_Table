# DB_Table
유저
- [유저 회원가입](#user_create)
- [유저 로그인](#user_login)
- [유저 정보 가져오기](#user_info)
- [유저 팔로우](#user_follow)
- [유저 팔로우 중인지 확인](#user_is_following)
- [유저 언팔로우](#user_unfollow)
- [유저 탈퇴](#user_remove)

글
- [글 쓰기](#bbs_write)
- [글 가져오기](#bbs_bring)
- [글 삭제](#bbs_remove)
- [글 수정](#bbs_rewrite)

그룹
- [그룹 생성](#room_create)
- [그룹 삭제](#room_remove)
- [그룹 정보](#room_info)
- [유저 등급 설정]($room_user_rank)
- [그룹 가입](#room_join)
- [그룹 탈퇴](#room_unjoin)
- [그룹 수정]

댓글
- [댓글 쓰기](#comment_write)
- [댓글 가져오기](#comment_bring)
- [댓글 삭제](#comment_remove)
- [댓글 수정]

기능
- [타임라인](#timeline)


---


## 유저
#### 유저 회원가입 <a id="user_create">
 http://lemontree.dothome.co.kr/pinbox/user/user_create

| param         | desc                       |
| :------------ | :------------------------- |
| user_name     | 이름                       |
| user_id       | 아이디                     |
| user_pw       | 비밀번호                   |
| user_email    | 이메일                     |
| user_sex      | 성별 (0 : 남자,   1 : 여자) |
| user_age      | 나이                       |
| user_phone    | 전화번호                   |
| user_profile  | 프로필 이미지               |

| return     | desc                          |
| :--------- | :---------------------------- |
| SUCCESS    | 성공                          |
| FAIL       | 실패                          |
| PHONE_FAIL | 이미 핸드폰 계정 있음          |
| EMAIL_FAIL | 이미 이메일 계정 있음          |
| ID_FAIL    | 이미 아이디 계정 있음          |

#### 유저 로그인 <a id="user_login">
 http://lemontree.dothome.co.kr/pinbox/user/user_login

| param      | desc         |
| :--------- | :----------- |
| user_id    | 유저 아이디   |
| user_pw    | 유저 비밀번호 |

| return     | desc         |
| :--------- | :----------- |
| SUCCESS    | 성공          |
| FAIL       | 실패          |

#### 유저 정보 가져오기 <a id="user_info">
 http://lemontree.dothome.co.kr/pinbox/user/user_info

| param      | desc         |
| :--------- | :----------- |
| user_id    | 유저 아이디   |

| return          | desc                |
| :-------------- | :------------------ |
| json(LA_USER)   | LA_USER 테이블 확인  |
| FAIL            | 실패                |

#### 유저 팔로우 <a id="user_follow">
 http://lemontree.dothome.co.kr/pinbox/user/user_follow

| param        | desc            |
| :----------- | :-------------- |
| user_token   | 유저            |
| target_token | 팔로우 할 타겟   |

| return     | desc         |
| :--------- | :----------- |
| SUCCESS    | 성공         |
| FAIL       | 실패         |

#### 유저 팔로우 중인지 확인 <a id="user_is_following">
 http://lemontree.dothome.co.kr/pinbox/user/user_is_following

| param        | desc          |
| :----------- | :------------ |
| user_token   | 유저          |
| target_token | 팔로우 할 타겟 |

| return           | desc          |
| :--------------- | :------------ |
| ALREADY_FOLLOW   | 팔로우 중임    |
| UN_FOLLOW        | 팔로우 중 아님 |
| FAIL             | 실패          |

#### 유저 팔로우 해제 <a id="user_unfollow">
 http://lemontree.dothome.co.kr/pinbox/user/user_unfollow

| param      | desc         |
| :--------- | :----------- |
| user_id    | 유저 아이디   |
| user_pw    | 유저 비밀번호 |

| return             | desc                 |
| :----------------- | :------------------- |
| SUCCESS            | 성공                 |
| FAIL               | 실패                 |
| ALREADY_UNFOLLOW   | 이미 언 팔로우 중임   |

#### 유저 팔로우 해제 <a id="user_remove">
 http://lemontree.dothome.co.kr/pinbox/user/user_remove

| param      | desc         |
| :--------- | :----------- |
| user_id    | 유저 아이디   |
| user_pw    | 유저 비밀번호 |
| user_phone | 유저 전화번호 |
| user_email | 유저 이메일   |

| return             | desc                        |
| :----------------- | :-------------------------- |
| SUCCESS            | 성공                        |
| FAIL               | 실패                        |
| WRONG_ID           | 아이디 또는 비밀번호가 틀림   |

> ※ 본 기능을 사용하기 전에 [#room_unjoin](#room_unjoin) 을 먼저 호출하고 SUCCESS 받아올 것

---

## 글
#### 글 쓰기 <a id="bbs_write">
 http://lemontree.dothome.co.kr/pinbox/bbs/bbs_write

| param      | desc         |
| :--------- | :----------- |
| room_token | 방 토큰       |
| content    | 내용          |
| writer     | 글쓴이 토큰   |

| return      | desc         |
| :--------- | :----------- |
| SUCCESS    | 성공          |
| FAIL       | 실패          |

#### 글 가져오기 <a id="bbs_bring">
 http://lemontree.dothome.co.kr/pinbox/bbs/bbs_bring

| param      | desc         |
| :--------- | :----------- |
| room_token | 방 토큰       |
| bbs_idx    | 게시글 번호   |

| return       | desc         |
| :----------- | :----------- |
| json(글정보) | PB_BBS 테이블 |
| FAIL         | 실패          |
| NOT_FOUND    | 글 못찾음     |

#### 글 삭제 <a id="bbs_remove">
 http://lemontree.dothome.co.kr/pinbox/bbs/bbs_remove

| param       | desc                        |
| :---------- | :-------------------------- |
| room_token  | 방 토큰                      |
| bbs_idx     | 게시글 번호                  |
| user_token  | 글삭제 요청한 사람의 토큰     |

| return      | desc         |
| :--------- | :------------ |
| SUCCESS    | 성공          |
| FAIL       | 실패          |
| NO_ACCESS  | 권한 없는 유저 |

#### 글 수정 <a id="bbs_rewrite">
 http://lemontree.dothome.co.kr/pinbox/bbs/bbs_rewrite

| param       | desc                        |
| :---------- | :-------------------------- |
| bbs_idx     | 게시글 번호                  |
| content     | 내용                        |
| user_token  | 글삭제 요청한 사람의 토큰     |

| return      | desc         |
| :--------- | :------------ |
| SUCCESS    | 성공          |
| FAIL       | 실패          |

---

## 그룹
#### 그룹 생성 <a id="room_create">
 http://lemontree.dothome.co.kr/pinbox/room/room_create

| param            | desc                              |
| :--------------- | :-------------------------------- |
| room_name        | 방 이름                           |
| room_manager     | 유저 토큰                          |
| room_min_age     | 최소 연령 설정                     |
| room_max_age     | 최대 연령 설정                     |
| room_profile     | 방 프로필 이미지                   |
| room_memlimit    | 방 인원수 제한                     |
| room_private     | 방 공개 여부 (기본 : false : 공개)  |
| room_tag_0 ~ 4   | 방 태그들                          |

| return      | desc                |
| :--------- | :------------------- |
| SUCCESS    | 성공                  |
| FAIL       | 실패                  |
| NAME_FAIL  | 이미 해당 이름이 있음  |

#### 그룹 삭제 <a id="room_remove">
 http://lemontree.dothome.co.kr/pinbox/room/room_remove

| param      | desc         |
| :--------- | :----------- |
| user_token | 유저 토큰     |
| room_token | 방 토큰       |

| return      | desc                           |
| :---------- | :----------------------------- |
| SUCCESS     | 성공                           |
| FAIL        | 실패                           |
| CANT_REMOVE | 없는 방 토큰이거나 매니저가 아님 |

#### 그룹 정보 <a id="room_info">
 http://lemontree.dothome.co.kr/pinbox/room/room_info

| param      | desc         |
| :--------- | :----------- |
| room_token | 방 토큰       |

| return           | desc                |
| :--------------- | :------------------ |
| json(PB_ROOM)    | PB_ROOM 테이블 확인  |
| FAIL             | 실패                 |

#### 유저 등급 설정 <a id="room_user_rank">
 http://lemontree.dothome.co.kr/pinbox/room/room_user_rank

| param        | desc         |
| :----------- | :----------- |
| user_token   | 유저 토큰     |
| room_token   | 방 토큰       |
| target_token | 대상 토큰     |
| rank         | 등급     |

| return           | desc                     |
| :--------------- | :----------------------- |
| SUCCESS          | PB_ROOM 테이블 확인       |
| FAIL             | 실패                     |
| RANK_FAIL        | 본인보다 높은 등급에 있음  |

#### 그룹 가입 <a id="room_join">
 http://lemontree.dothome.co.kr/pinbox/room/room_join

| param      | desc         |
| :--------- | :----------- |
| user_token | 유저 토큰     |
| room_token | 방 토큰       |

| return      | desc         |
| :--------- | :----------- |
| SUCCESS   | 성공          |
| FAIL       | 실패          |
| MEM_LIMIT  | 인원 초과      |
| NOT_FOUND_ROOM  | 없는 방      |

#### 그룹 탈퇴 <a id="room_unjoin">
 http://lemontree.dothome.co.kr/pinbox/room/room_unjoin

| param      | desc         |
| :--------- | :----------- |
| user_token | 유저 토큰     |
| room_token | 방 토큰       |

| return          | desc         |
| :---------------| :----------- |
| SUCCESS         | 성공         |
| FAIL            | 실패         |
| NOT_FOUND_ROOM  | 없는 방      |

---

## 댓글
#### 댓글 쓰기 <a id="comment_write">
 http://lemontree.dothome.co.kr/pinbox/comment/comment_write

| param      | desc            |
| :--------- | :-------------- |
| bbs_idx    | 글 idx          |
| content    | 내용            |
| writer     | 작성한 유저 토큰 |

| return     | desc         |
| :--------- | :----------- |
| SUCCESS    | 성공         |
| FAIL       | 실패         |

#### 댓글 가져오기 <a id="comment_bring">
 http://lemontree.dothome.co.kr/pinbox/comment/comment_bring

| param      | desc         |
| :--------- | :----------- |
| bbs_idx    | 글 idx        |

| return              | desc                    |
| :------------------ | :---------------------- |
| json(PB_COMMENT)    | PB_COMMENT 테이블 확인   |
| FAIL                | 실패                     |
| NOT_FOUND           | 댓글 없음                |

#### 댓글 삭제 <a id="comment_remove">
 http://lemontree.dothome.co.kr/pinbox/comment/comment_remove

| param         | desc                       |
| :------------ | :------------------------- |
| comment_idx   | 댓글 idx                   |
| user_token    | 글삭제 요청한 사람의 토큰    |

| return              | desc                    |
| :------------------ | :---------------------- |
| SUCCESS             | 성공                    |
| FAIL                | 실패                    |
| NO_ACCESS           | 권한 없는 유저           |

---

## 기능
#### 타임라인 <a id="timeline">
 http://lemontree.dothome.co.kr/pinbox/edition/timeline

| param      | desc         |
| :--------- | :----------- |
| user_id    | 유저 아이디   |
| bbs_idx    | 글 idx       |

| return       | desc              |
| :----------- | :---------------- |
| json(PB_BBS) | PB_BBS 테이블 확인 |
| FAIL         | 실패               |
