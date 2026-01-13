function listen(){
    db.ref(room).on("value", snap=>{
        const data=snap.val();
        if(!data) return;

        turn=data.turn;

        data.board.forEach((v,i)=>{
            board.children[i].innerText =
              v==="X"?"❌":v==="O"?"⭕":"";
        });

        if(data.winner){
            if(data.winner==="draw"){
                statusText.innerText="🤝 ড্র";
                drawSound.play();
            }
            else if(data.winner===player){
                statusText.innerText="🎉 তুমি জিতেছো!";
                winSound.play();
            }
            else{
                statusText.innerText="😈 তুমি হেরে গেছো";
                loseSound.play();
            }
        }
        else{
            if(turn===player){
                statusText.innerText="👉 তোমার চাল";
                turnSound.play();
            }else{
                statusText.innerText="⏳ অপেক্ষা করো";
            }
        }
    });
}
