---
layout: post
title: "Multi email validation"
author: "praconfi"
tags: Javascript
---
업무용으로 보내는 메일을 단 한명에게만 보내는 경우는 적다. 업무 관련 참조인들이 많기 때문이다.  
그래서 보통 ';'로 메일들을 구분해 여러개의 메일 주소를 적는데, 작성과정에서 실수를 잡기위해 유효성 검사를 추가한다.  
해당 서버는 ','로 구분을 하기 때문에 그에 맞춰 작성되었다.  
로직은 ','로 메일들을 구분한 뒤, 정규표현식으로 유효성 검사를 한다.  
성공한다면 메일전송 로직은 이어지고, 실패한다면 검증에 실패한 메일을 alert로 보여주고 메일전송로직은 이어지지 않는다

> 정규표현식은 https://regexper.com/ 에서 시각적으로 확인해 볼 수 있다
![image](https://user-images.githubusercontent.com/64571546/135945034-f13c5f86-bddf-4469-82a7-a4ad997231ae.png)


```js
function checkEmailValidity(emailList) {
    let reg = /^.+?@.+?\.\w{2,}$/i;
    let emailArr;
    if (emailList.indexOf(";") < emailList.indexOf("@")) {
        //assume only one email address on the list
        emailArr = [emailList];
    } else {
        emailArr = emailList.split(";")
    }
    let isValid = true;
    emailArr.forEach(function(addr) {
        if (reg.test(addr) === false) {
            alert("이메일을 확인해 주세요: " + addr + "\n이메일은 , 로 구분됩니다");
            isValid = false;
        }
    })
    return isValid;
}

const sendRejectEmail = () => {
	if(confirm('이메일을 발송하시겠습니까?')){

		// 이메일 validation 추가(다중이메일은 ','로 구분된다)
		let emailAddresses = document.getElementById('reject_email').value;
		if(!checkEmailValidity(emailAddresses)){
			return;
		}

		try{
            ...
		
		}
		catch(e)
		{

		}
	}
};

```