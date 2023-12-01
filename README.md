<h3>주요 기능</h3>
<hr>
ToyConn 서비스의 핵심 기능은 로그인 이후 해당 유저 동네에 위치한 장난감 표시 기능, 장난감 위치 확인 후 채팅, 그리고 결제 기능입니다.
<h4>
    로그인기능
</h4>
<h4>
    동네에 위치한 장난감 표시 기능
</h4>
<img src="https://github.com/jangjunhyu/-/assets/120622212/0036a59d-8b67-470d-92b7-30914870d1f7">

우편주소는 불변값이기 때문에 데이터 베이스에 저장된 장난감 전부 출력하고 유저의 주소에 맞는 장난감만 출력
~~~java
<%
				for (int i = 0; i < list.size(); i++) {
					if (list.get(i).getAddress().contains(result) && !list.get(i).getUser_id().equals(id)) {
				%>
				<div
					class="col-sm-6 col-md-4 col-lg-3 p-b-35 isotope-item <%=list.get(i).getCategory()%>">
					<div class="block2">
						<div class="block2-pic hov-img0">
							<!-- 상품 사진 -->
							<img src="images/crolling/<%=list.get(i).getImage_file()%>"
								alt="IMG-PRODUCT">
						</div>
						<div class="block2-txt flex-w flex-t p-t-14">
							<div class="block2-txt-child1 flex-col-l ">
								<!-- 상품명 -->
								<a href="toy_info.jsp?p_num=<%=list.get(i).getP_num()%>"
									class="stext-104 cl4 hov-cl1 trans-04 js-name-b2 p-b-6"> <%=list.get(i).getP_name()%>
								</a>
								<!-- 가격 -->
								<span class="stext-105 cl3"> <%=list.get(i).getRent_price()%>원
								</span>
							</div>
							<!-- 하트 아이콘 -->
							<div class="block2-txt-child2 flex-r p-t-3">
								<a href="#"
									class="btn-addwish-b2 dis-block pos-relative js-addwish-b2">
									<img class="icon-heart1 dis-block trans-04"
									src="images/icons/icon-heart-01.png" alt="ICON"> <img
									class="icon-heart2 dis-block trans-04 ab-t-l"
									src="images/icons/icon-heart-02.png" alt="ICON">
								</a>
							</div>
						</div>
					</div>
				</div>
				<%}}%>
~~~

<h4>장난감 위치 확인 기능</h4>
<hr>
<ul>
	<li>장난감 정보 클릭시 해당 장난감 정보(제품명, 가격, 세부내용, 유저) 표현</li>
	<li>정보 페이지 '위치확인'버튼 클릭시 오버레이로 위치정보 표현</li>
</ul>

<img src="https://github.com/jangjunhyu/-/assets/120622212/22309cc6-fea2-4105-9105-6faec8b21106">

~~~java
<script type="text/javascript"
		src="//dapi.kakao.com/v2/maps/sdk.js?appkey=c4761ef1bd1bad042ac92bb3429a6cd9&libraries=services"></script>
	<script type="text/javascript">
		function moveChat() {
			document.querySelector(
			"#goChat").submit();
		}
	</script>
	<script>
	var mapContainer = document.getElementById('map'), 
	mapOption = {
	    center: new kakao.maps.LatLng(37.566826, 126.9786567), 
	    level: 3 
	};  
   
	var map = new kakao.maps.Map(mapContainer, mapOption); 

	var geocoder = new kakao.maps.services.Geocoder();

	geocoder.addressSearch('<%=Taddress%>'
			, function(result, status) {

			if (status === kakao.maps.services.Status.OK) {

				var coords = new kakao.maps.LatLng(result[0].y, result[0].x);

				var marker = new kakao.maps.Marker({
					map : map,
					position : coords
				});

				map.setCenter(coords);
			}
		});
	</script>
~~~

<h4>채팅 기능</h4>
<ul>
	<li>사용자가 상품정보 페이지에 존재하는 채팅하기 버튼 클릭</li>
	<li>채팅 페이지로 이동하여 해당 장난감 소유 유저와 채팅</li>
	<li>입력 창에 채팅 내용 입력 후 전송 버튼 클릭</li>
	<li>DB에 저장 후 값을 바로 받아와 sendRedirect 형식으로 데이터 전송</li>
</ul>
<img src="https://github.com/jangjunhyu/-/assets/120622212/66d0ce2c-2040-4847-b104-49ea208434ac">
