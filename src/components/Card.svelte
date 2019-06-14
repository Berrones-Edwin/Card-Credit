<script>
    import Alert from './Alert.svelte';
    import Modal from './Modal.svelte';

    let numberCard ='';
    let nameCard='';
    let monthCard='';
    let yearCard='';
    let cvvCard='';
    let validateForm=true;
    let src = '';
    let firstNumber='';

    // Alert
    const alertProops={
        title:'',
        description:'',
        type:'',
        closeModal:true
    }

    // Validations
    let numberCardValidate =false;
    let nameCardValidate=false;
    let monthCardValidate=false;
    let yearCardValidate=false;
    let cvvCardValidate=false;

    const changeLogo = () =>{
        firstNumber = numberCard.slice(0,1);
        
        if(Number(firstNumber)===3){
           src ='img/american.png';
           
        } else  if(Number(firstNumber)===4){
            src ='img/visa.png';
            
        }else  if(Number(firstNumber)===5){
            src ='img/master.png';
           
        } else{
            src ='';

        }
    }

    const onlyNumber = (myInput) =>{
        if(myInput.length ===0 || myInput==='') return; 

        if(!myInput.match(/^\d+/))
        {

            document.getElementById('myModal').classList.remove('close');

            alertProops.title='Error';
            alertProops.description='Solo se permiten números';
            alertProops.type='danger';
            alertProops.closeModal=false;


            return true;
            
        }
    }

    const formattingNumberCard = () =>{
        changeLogo();
        if(onlyNumber(numberCard)) numberCard='';
        if(numberCard.length===4) numberCard+=' ';
        else if(numberCard.length===9) numberCard+=' ';
        else if(numberCard.length===14) numberCard+=' ';
    }  

    const formattingMonthCard = () =>{

         if(onlyNumber(monthCard)) monthCard='';

         let aux = monthCard;
         let number = [1,2,3,4,5,6,7,8,9];

         for(let i = 0 ; i< number.length;i++)
             if(Number(monthCard) === number[i])
                 monthCard = '0' + aux;

             
    }
    const formattingYearCard = () =>{

        if(onlyNumber(yearCard)) yearCard='';
    }
    const formattingCvvCard = () =>{

        if(onlyNumber(cvvCard)) cvvCard='';
    }



    const addCardCredit = (e) =>{

        e.preventDefault();
        if(numberCard.length>0 && nameCard.length>0 && monthCard.length>0 && yearCard.length>0 && cvvCard.length>0){
            
            if(numberCard.length<19){
                const x = document.getElementById('numberCard')
                console.log(x);
                x.classList.add('inputInvalid');

                numberCardValidate =true;
                return;
            }
            if(monthCard.length <2 || monthCard.length > 2){
                
                document.getElementById('monthCard').classList.add('inputInvalid');
                 monthCardValidate=true;
                 return;
            }
            if(yearCard.length <4 || yearCard.length > 4){
                
                document.getElementById('yearCard').classList.add('inputInvalid');
                yearCardValidate=true;
                return;
            }
            if(cvvCard.length <3 || cvvCard.length > 3){
                
                document.getElementById('cvvCard').classList.add('inputInvalid');
                cvvCardValidate=true;
                return;
            }

            numberCardValidate =false;
            nameCardValidate=false;
            monthCardValidate=false;
            yearCardValidate=false;
            cvvCardValidate=false;

            document.getElementById('myModal').classList.remove('close');
            alertProops.title='Correcto';
            alertProops.description='El método de pago se agregó satisfactoriamente';
            alertProops.type='success';
            alertProops.closeModal=false;

        }else{
            numberCardValidate =true;
            nameCardValidate=true;
            monthCardValidate=true;
            yearCardValidate=true;
            cvvCardValidate=true;
        }

    }

</script>

<style>
    h2{
        margin: 0;
        padding: 0;
    }
    .title{
        text-align: center;
        margin-bottom: 1rem;
        letter-spacing: 2px;
    }
    /*ESTILOS TARJETA*/

    .card-sideLeft{
        height: 200px;
        margin-bottom: 2rem;
    }
    .sideleft__creditCard{
        height: 200px;
        background-color: #ccc;
        width:90%;
        margin:0 auto;
        border-radius: 10px;
        box-shadow: 4px 3px 4px 0px rgb(112, 109, 109);

    }
    .backgroundAmerican{
        background-color: #a3d7f5;
    }
    .backgroundVisa{
        background-color:#619edb ;
        color:#FFF;
    } 
    .backgroundMaster{
        background-color:#f5c668 ;
    }
    .creditCard__container{
        width:100%;
        display: flex;
        flex-direction: row;
        justify-content: space-between;
        height:  80px;
    }
    .creditCard__container:nth-child(2){
        display: block;
        
    }
    .creditCard__container:nth-child(2) p {
        letter-spacing: 2px;
        margin-left: 1rem;
        margin-bottom: -0.5rem;
     }

    .creditCard__pin{
        background-color: #dfa73a;
        width: 100px;
        height: 3.5rem;
        border-radius: 10px;
        margin-top:1rem;
        margin-left: 1rem;
        display: grid;
        grid-template-columns: repeat(2,1fr);
        grid-template-rows: repeat(3,1fr);
    }
    .creditCard__pin section{
        width:  20px;
        height: 10px;
        border-radius:2px;
        background-color: #c09133;
        margin:5px auto 0;
    }

    .creditCard__logo{
        width: 60px;
        height:  60px;
        margin-right: 1rem;

    }
    /*ESTILOS FORMULARIO*/
   
    .form__container{
        width: 100%;
        margin-bottom: 1rem;

    }
    .form__container label,
    .form__container input{
        width: 100%;
        
    }
    .form__container label{
        margin-bottom: .5rem;
        letter-spacing: 1px;
    }

    input:focus{
        border:none;
        outline: none;
        outline:1px solid #ccc;
    }
    .sideRight__form button{
        width: 100%;
        border-radius:10px;
        background-color: #6c757d;
        border-color: #6c757d;
        color:#FFF;
    }
    .sideRight__form button:hover{
        color: #fff;
        background-color: #5a6268;
        border-color: #545b62;
    
    }

    @media (min-width:576px ) {
        /* .title{ color:yellow} */

        .card{
            width: 90%;
            margin:0 auto;
            display: flex;
            justify-content: space-around;
            align-items: center;

        }
        .sideleft__creditCard{
            height: 250px;
            width: 400px;
        }
        .creditCard__pin{
            width: 80px;
            height: 60px;
        }

        .creditCard__logo{
            width: 80px;
            height:  70px;
            margin-top: 1rem;

        }
        .creditCard__container:nth-child(1){
            margin-bottom: 4rem;
        }

        /* Formulario */
        
        .form__container:nth-child(3){
            display: flex;
            flex-wrap: wrap;
        }
         .form__container:nth-child(3) label{
             width: 100%;
         }
         .form__container:nth-child(3) input{
             width: 45%;
             margin-right: 1rem;
             
         }

        /* .alert{
            width:90%;
        } */

    }


    .inputInvalid{
        border:1px solid red;
    }

</style>

<h2 class="title">Nuevo método de pago</h2>


<Modal {...alertProops}  />

<section class="card">
    <div class="card-sideLeft">
       <div class="sideleft__creditCard" 
            class:backgroundAmerican={Number(firstNumber)===3} 
            class:backgroundVisa={Number(firstNumber)===4}
            class:backgroundMaster={Number(firstNumber)===5}
            >

            <div class="creditCard__container">
                <div class="creditCard__pin">
                    <section></section>
                    <section></section>
                    <section></section>
                    <section></section>
                    <section></section>
                    <section></section>
                </div>
                <img {src} class="creditCard__logo" alt="{nameCard}">
            </div>

            <div class="creditCard__container">
                <p>{ numberCard || 'xxxx xxxx xxxx xxxx' }</p>
                <p>{ nameCard || 'Nombre del tarjeta habiente' }</p>
                <p>
                    { monthCard || 'MM' } /
                    { yearCard || 'YYYY' }
                </p>
            </div>
       </div>
    </div>
    <div class="card-sideRight">
        <form action="" class="sideRight__form">

            <div class="form__container">

                <label for="numberCard">Número de la tarjeta</label>
                <input type="text"
                        placeholder="xxxx xxxx xxxx xxxx"
                        minlength="19" maxlength="19"
                        name="numberCard"
                        bind:value={numberCard}
                        required
                        autocomplete="off"
                        on:keyup={formattingNumberCard}
                        id="numberCard"
                        class:inputInvalid={numberCardValidate}>
                {#if numberCardValidate}
                    <Alert description={'Campo es Invalido. Escriba los 16 digitos de su tarjeta.'} />
                {/if}
            </div>

            <div class="form__container">

                <label for="nameCard">Nombre del tarjeta habiente</label>
                <input type="text" 
                        name="nameCard"  
                        bind:value={nameCard}
                        required
                        autocomplete="off"
                        placeholder="Nombre del tarjeta habiente "
                        id="nameCard"
                        class:inputInvalid={nameCardValidate}>
                {#if nameCardValidate}
                     <Alert description={'Campo es Invalido.Introuduzca su nombre completo'} />
                {/if}
            </div>

            <div class="form__container">

                <label for="monthCard"> Fecha de Vencimiento</label>
                <input type="text" 
                        placeholder="MM"   
                        minlength="2" 
                        maxlength="2"
                        name="monthCard"
                        bind:value={monthCard}
                        pattern="\d*"
                        required
                        autocomplete="off"
                        id="monthCard"
                        on:keyup={formattingMonthCard}
                        class:inputInvalid={monthCardValidate}>
                    

                <input type="text" 
                        placeholder="AAAA" 
                        maxlength="4" 
                        minlength="4"
                        name="yearCard"  
                        bind:value={yearCard}
                        pattern="\d*"
                        required
                        autocomplete="off"
                        id="yearCard"
                        on:keyup={formattingYearCard}
                        class:inputInvalid={yearCardValidate}>

            </div>
             {#if monthCardValidate || yearCardValidate }

                <Alert description={'Campo es Invalido.Verifique si el mes  y año son correctos.'} />

            {/if}

            <div class="form__container">
                <label for="cvvCard">CVV</label>
                <input type="text" 
                        placeholder="***" 
                        maxlength="3" 
                        minlength="3"
                        name="cvvCard"  
                        bind:value={cvvCard}
                        required
                        autocomplete="off"
                        id="cvvCard"
                        on:keyup={formattingCvvCard}
                        class:inputInvalid={cvvCardValidate}>

                 {#if cvvCardValidate }
                    <Alert description={'Campo es Invalido. Escriba los 3 digitos de su tarjeta.'} />
                {/if}

            </div>
            <button class="btn" on:click={addCardCredit}>
                Agregar Método de pago
            </button>

        </form>
    </div>
</section>
