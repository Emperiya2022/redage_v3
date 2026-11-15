<script>
	let isMultiplayer = window.mp && window.mp.events;

	document.imgurClientId = "ec243f05d2bc44b";

	import 'lang/index'
	//import '@/advertisement';
	import router from 'router';
	import axios from 'axios';
	import '@/views/assets/css/main.js';
	import '@/views/assets/fonts/main.js';
	import 'components/rangeslider/main.css'
	import 'api/events'
	import 'api/imgSave'
	import 'store/customization';

	import 'store/account';
    import { charIsPet } from 'store/chars'
	import 'store/loader';
	import 'store/keys';
	import { inVehicle, isInputToggled } from 'store/hud';
	import 'store/quest';
	import 'store/settings';
    import { storeAnimBind } from 'store/animation'
    import { newsData } from 'store/news'

    import { executeClient } from 'api/rage'
	import ViewContainer from 'components/viewcontainer/index.svelte';
	import PopusContainer from 'components/popuscontainer/index.svelte';
	import FadeContainer from 'components/fadecontainer/index.svelte';
	import FilterBlur from './components/filterblur/index.svelte';

	//Игрока'
	import PlayerBattlePass from '@/views/player/battlepass/index.svelte';
	import PlayerRentCar from '@/views/player/rentcar/index.svelte';
	import PlayerAuthentication from '@/views/player/newauthentication/index.svelte';
	import PlayerCustomization from '@/views/player/customization/index.svelte';
	import PlayerAtm from '@/views/player/atm/index.svelte';
	import PlayerBinder from '@/views/player/binder/index.svelte';
	import PlayerDocumets from '@/views/player/documets/index.svelte';
	import PlayerClothesEditor from '@/views/player/clothesEditor/index.svelte';
	import PlayerCarMarket from '@/views/player/carmarket/index.svelte';
	import PlayerHelp from '@/views/player/help/index.svelte';
	import PlayerGameMenu from '@/views/player/menu/index.svelte';
	import PlayerLicense from '@/views/player/license/index.svelte';
	import PlayerPassport from '@/views/player/passport/index.svelte';
	import PlayerDropinfo from '@/views/player/dropinfo/index.svelte';
	import PlayerHud from '@/views/player/hudevo/index.svelte';
	import PlayerLift from '@/views/player/lift/index.svelte';
	import PlayerGasStation from '@/views/player/gasStation/index.svelte';
	import PlayerBreakingLock from '@/views/player/breakingLock/index.svelte';
	import PlayerTransfer from '@/views/player/transfer/index.svelte';
	import PlayerJobSelector from '@/views/player/jobselector/index.svelte';
	import PlayerReports from '@/views/player/reports/index.svelte';

	//import PlayerNewYearStats from '@/views/player/newyearstats/index.svelte';
	import PlayerAnimations from '@/views/player/animations/index.svelte';
	import PlayerOresSale from '@/views/player/oressale/index.svelte';
	import PlayerMetro from '@/views/player/metro/index.svelte';
	import PlayerWedding from '@/views/player/wedding/index.svelte';
	import PlayerTickets from '@/views/player/tickets/index.svelte';
	import PlayerRestart from '@/views/player/restart/index.svelte';

	//Администрации

	//import AdminPlayersView from '@/views/admin/playersView/index.svelte';
	//import AdminReport from '@/views/admin/report/index.svelte';

	//Бизнес
	import BusinessAutoShop from '@/views/business/autoshop/index.svelte';
	import BusinessWeaponShop from '@/views/business/weaponshop/index.svelte';
	import BusinessPetShop from '@/views/business/petshop/index.svelte';
	import BusinessMenu from '@/views/business/menu/index.svelte';
	import BusinessNewPetShop from '@/views/business/newpetshop/index.svelte';
	import BusinessClothes from '@/views/business/clothes/index.svelte';

	//Фракции
	// /import FractionsAdverts from '@/views/fractions/adverts/index.svelte';
	import FractionsBSearch from '@/views/fractions/bsearch/index.svelte';
	import FractionsMats from '@/views/fractions/mats/index.svelte';
	import FractionsCraft from '@/views/fractions/craft/index.svelte';
	import FractionsCreate from '@/views/fractions/create/index.svelte';
	import FractionsStock from '@/views/fractions/stock/index.svelte';
	import FractionsPolicecomputer from '@/views/fractions/policecomputer/index.svelte';
	import FractionsTicket from '@/views/fractions/ticket/index.svelte';
	import FractionsBortovoi from '@/views/fractions/bortovoi/index.svelte';
	import FractionsWeazelNews from '@/views/fractions/weazelnews/index.svelte';
	import FractionsWar from '@/views/fractions/war/index.svelte';

	//Казино
	import CasinoBlackjack from '@/views/casino/blackjack/index.svelte';
	import CasinoHorse from '@/views/casino/horse/index.svelte';
	import CasinoJacpot from '@/views/casino/jacpot/index.svelte';
	import CasinoRoullete from '@/views/casino/roullete/index.svelte';

	import VehicleAir from '@/views/vehicle/air/index.svelte';
	import VehicleLsCustom from '@/views/vehicle/lscustom/index.svelte';

	//Games
	import GamesOtherMain from '@/views/games/other/index.svelte';
	import GamesOtherMafia from '@/views/games/other/mafia/index.svelte';
	import GamesOtherLobby from '@/views/games/other/lobby/index.svelte';

	//
	import DonateMain from '@/views/donate/main/index.svelte';
	//import DonateCards from '@/views/donate/cards/index.svelte';
	import DonateSapper from '@/views/donate/sapper/index.svelte';


	import QuestsDialog from '@/views/quests/dialog/index.svelte';

	//import QuestsDialog1 from '@/views/quests/questsnew/questsnewdialog/index.svelte';
	//import QuestsDialog2 from '@/views/quests/questsnew/questsnewlist/index.svelte';
	//import QuestsDialog3 from '@/views/quests/questsnew/questsprise/index.svelte';

	import EventsValentine from '@/views/events/valentine/index.svelte';

	//House
	import HouseMenu from '@/views/house/menu/index.svelte';
	import HouseRielt from '@/views/house/rieltagency/index.svelte';
	import HouseBuy from '@/views/house/buymenu/index.svelte';
	import HouseFurniture from '@/views/house/furniture/index.svelte';


	const Views = {
		PlayerBattlePass,
		//PlayerNewAuthentication,
		PlayerAuthentication,//Авторизация, выбор спавна, выбор чара
		PlayerCustomization,//кастомизация
		PlayerAtm,//Банкоматы
		PlayerBinder,//биндер
		PlayerDocumets,//Документы фракционные
		PlayerClothesEditor,//Эдитор одежды (только для тестов)
		PlayerCarMarket,// авторынок НУЖНО СДЕЛАТЬ СЕЙЧАС НЕ РАБОТАЕТ
		PlayerHelp,//Хелп
		PlayerLicense,//Лицензии
		PlayerPassport,//паспорт
		PlayerTransfer,// Перенос
		PlayerJobSelector,//Выбор работы
		PlayerReports,//Репорты
		PlayerDropinfo,//Подсказки для кнопки 'поставить'
		PlayerLift,//Лифт
		PlayerGasStation,//Заправка
		PlayerBreakingLock,//Взлом сейфа
		PlayerRentCar,//Аренда авто
		//PlayerNewYearStats,
		PlayerAnimations,
		PlayerOresSale,//Продажа руд
		PlayerMetro,
		PlayerWedding,
		PlayerTickets,
		PlayerRestart,

		BusinessAutoShop,
		BusinessWeaponShop,
		BusinessPetShop,
		BusinessMenu,//24/7, черный рынок
		BusinessNewPetShop, //новый магазин животных
		BusinessClothes,

		//FractionsAdverts,//лс невс
		FractionsBSearch, //Протокол обыска
		FractionsMats,//Материал
		FractionsCraft,//Крафт
		FractionsStock,//Склад
		FractionsPolicecomputer,
		FractionsTicket,
		FractionsBortovoi,
		FractionsWeazelNews,
		FractionsWar,
		FractionsCreate,

		CasinoBlackjack,
		CasinoHorse,
		CasinoJacpot,
		CasinoRoullete,

		//AdminPlayersView,//Не работает
		//AdminReport,

		VehicleAir,
		VehicleLsCustom,//Тюнинг

		GamesOtherMain,//Меню основных мероприятий
		GamesOtherMafia,//Игра Мафия
		GamesOtherLobby,//Меню лобби

		DonateMain,
		//DonateCards,
		DonateSapper,

		QuestsDialog,
		//QuestsDialog1,
		//QuestsDialog2,
		//QuestsDialog3,
		EventsValentine,

		HouseBuy,
		HouseMenu,
		HouseRielt,
		HouseFurniture
	}
	
	//window.router.setView("PlayerAuthentication")
	window.router.setHud()
	//window.router.setView("FractionsCreate")
	//window.router.close()
	//window.router.updateStatic("PlayerGameMenu");

	//Popups
	import PopupInput from '@/popups/input/index.svelte';
	import PopupConfirm from '@/popups/confirm/index.svelte';
	import HospitalPopupConfirm from '@/popups/confirm/hospital_index.svelte';
	import PopupDonate from '@/popups/donate/index.svelte';
	import PopupDeath from '@/popups/death/index.svelte';
	import CircleMenu from '@/popups/circle/index.svelte';
	//import PopupAuth from '@/popups/auth/index.svelte';
	import PopupMain from '@/popups/main/index.svelte';
	import PopupSelect from '@/popups/select/index.svelte';
	import PopupRoulette from '@/popups/roulette/index.svelte';
	import PopupUpgrade from '@/popups/upgrade/index.svelte';
	import PopupCamera from '@/popups/camera/index.svelte';
	import PopupWar from '@/popups/war/index.svelte';

	const Popus = {
		PopupConfirm,
		HospitalPopupConfirm,
		PopupInput,
		PopupDeath,
		PopupDonate,
		CircleMenu,
		PopupSelect,
		//PopupAuth,
		PopupMain,
		PopupUpgrade,
		PopupRoulette,
		PopupCamera,
		PopupWar
	}
	//window.router.setPopUp("PopupWar")

	/*axios.get(`https://redage.net/?getnews=1`).then(res => {
		if (res && res.data && res.data.result) {
			newsData.set(res.data.result);
		}
	});*/

	import { onMount } from 'svelte';

	onMount(() => {
		executeClient ("client:OnBrowserInit");
		if (!isMultiplayer) {
			const body = document.querySelector('body');
            body.style.background = "black";
			window.FadeScreen (false, 0);
			window.initCustomizations ();
			window.events.callEvent("cef.inventory.InitData", '{"accessories":[{"SqlId":5976,"ItemId":-4,"Count":1,"Data":"83_1_True","Index":9,"Price":0},{"SqlId":5972,"ItemId":-6,"Count":1,"Data":"79_0_[...]');
			window.events.callEvent("cef.inventory.InitOtherData", 10, 1, '[{"SqlId":29,"ItemId":220,"Count":1,"Data":"Camry","Index":0,"Price":0},{"SqlId":30,"ItemId":220,"Count":1,"Data":"Quad1","Index"...');

			//window.hudStore.isHudNewPhone(true)

			for(let i = 0; i < 9; i++)
				window.chat.addMessage(i + " test тектс тектс тектс тектс тектс тектс тектс тектс тектс тектс тектс тектс тектс тектс т�[...");

			isInputToggled.set(true)
		} else {
			//window.router.close ();
			window.router.setView('PlayerAuthentication');
		}
	});
	//window.router.updateStatic("PlayerGameMenu", [{ActorName:"", Line:""}])

    import keys from 'store/keys'

	let isKeyBind = -1;
	let isKeyBindUse = false;
	const keyToBind = {
		48: 9,
		49: 0,
		50: 1,
		51: 2,
		52: 3,
		53: 4,
		54: 5,
		55: 6,
		56: 7,
		57: 8,
	}

	let isKeyDown = false;

	window.SetBindToKey = (key) => {
		if (key === -1)
			isKeyDown = false;
		else
			isKeyDown = true;

		isKeyBind = key;

		executeClient ("setBindToKey", key);
	}

	let fastClickData = {};

	const FastClick = (key, awaitFunc, Func) => {
		if (fastClickData [key]) {
			clearTimeout(fastClickData [key]);
			delete fastClickData [key];
			Func()
		} else {
			fastClickData [key] = setTimeout(() => {
				delete fastClickData [key];
				awaitFunc ();
			}, 250)
		}
	}

	const handleKeydown = (event) => {
		if (!$router.PlayerHud)
			return;
		else if ($inVehicle || $isInputToggled)
			return;
		const { keyCode } = event;

		if (isKeyBind !== -1) {
			if (isKeyBind === $keys[8]) {
				const anim = $storeAnimBind;
				if (anim) {
					for (let i = 0; i < 11; i++) {
						if (keyCode === (48 + i) && anim[keyToBind [48 + i]] && anim[keyToBind [48 + i]].split('_')) {
							executeClient ("client.animation.play", anim[keyToBind [48 + i]]);
							isKeyBindUse = true;
							window.SetBindToKey (-1);
							return;
						}
					}
				}
			} else if (isKeyBind === $keys[55] && keyCode === $keys[55]) {
				window.hudStore.isAnimal (false);
				executeClient ("client.pet.isUse", false);
				window.SetBindToKey (-1);
			}
		} else {
			if (isKeyDown)
				return;

			if (keyCode === $keys[8]) {
				isKeyBindUse = false;
				window.SetBindToKey ($keys[8]);
			}
			else if (keyCode === 32) {
				executeClient ("client.animation.stop");
			}
			else if($charIsPet && keyCode === $keys[55]) {
				window.hudStore.isAnimal (true);
				executeClient ("client.pet.isUse", true);
				window.SetBindToKey ($keys[55]);
			}
		}
	}

	const handleKeyup = (event) => {
		if (!isKeyDown)
			return;

		if (!$router.PlayerHud)
			return;
		else if ($inVehicle || $isInputToggled)
			return;

		const { keyCode } = event;

		if (keyCode === $keys[8]) {
			window.SetBindToKey (-1);
			if (!isKeyBindUse) {
				executeClient ("client.animation.open");
			}
		}
	}



</script>

<svelte:window on:keydown={handleKeydown} on:keyup={handleKeyup} />

<div class="cef-shell">
	<div class="cef-shell__glow"></div>
	<div class="cef-shell__grid"></div>

	<FadeContainer />
	<ViewContainer visible={Popus[$router.popup] ? true : false} opacity={$router.opacity && $router.popup !== "PopupCamera" ? 1 : 0}>
		{#if Views[$router.view]}
		<svelte:component this={Views[$router.view]} viewData={$router.viewData} />
		{/if}
		<!--<UiFilter/>-->
		<PlayerGameMenu visible={$router.PlayerGameMenu} />
		<PlayerHud visible={$router.PlayerHud} />
		<!--<svelte:component this={Views.PlayerGameMenu} visible={$router.PlayerGameMenu} />
		<svelte:component this={Views.PlayerHud} visible={$router.PlayerHud} />
		<svelte:component this={Views.QuestsDialog} />-->
	</ViewContainer>

	<PopusContainer visible={Popus[$router.popup] ? true : false} opacity={$router.opacity}>
		<svelte:component this={Popus[$router.popup]} popupData={$router.popupData} popupFunc={$router.popupFunc} />
	</PopusContainer>
</div>
