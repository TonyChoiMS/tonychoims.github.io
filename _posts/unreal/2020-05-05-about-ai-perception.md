---
layout: post
title:  "Unreal Engine AI Perception"
date:   2020-05-05
desc: "Unreal Engine AI Perception"
keywords: "UnrealEngine"
categories: [Unreal]
tags: [Unreal,UnrealEngine]
icon: icon-html
---

In addition to Behavior Trees which can be used to make decisions on which logic to execute, and the Environmental Query System (EQS) used to retrieve information about the environment; another tool you can use within the AI framework which provides sensory data for an AI is the AI Perception System. This provides a way for Pawns to receive data from the environment, such as where noises are coming from, if the AI was damaged by something, or if the AI sees something. This is accomplished with the AI Perception Component that acts as a stimuli listener and gathers registered Stimuli Sources.
  
AI가 실행할 로직에 대한 결정을 내리는 데 사용할 수 있는 비헤이비어 트리와 환경에 대한 정보를 검색하는 데 사용되는 환경 쿼리 시스템 (EQS) 외에 AI 프레임 워크 내에서 사용할 수 있는 AI에 대한 감각 데이터를 제공하는 또 다른 도구는 AI Perception System입니다. 이것은 폰이 노이즈가 발생하는 곳, AI가 무언가에 의해 손상된 경우 또는 AI가 무언가를 보는 것과 같은 것으로부터 데이터를 수신하는 방법을 제공합니다. 이것은 자극 청취자 역할을하고 등록 된 자극 소스를 수집하는 AI Perception Component로 구성됩니다.
  
  
When a stimuli source is registered, the event On Perception Updated (or On Target Perception Updated for target selection) is called which you can use to fire off new Blueprint Script and (or) update variables that are used to validate branches in a Behavior Tree.
  
Stimuli Source가 등록되면, 새로운 블루 프린트 스크립트를 시작하고 행동 트리에서 브랜치를 검증하는 데 사용되는 변수를 업데이트하는 데 사용할 수있는 On Perception Updated (또는 대상 선택에 대한 On Target Perception Updated) 이벤트가 호출됩니다.
  
## AI Perception Component
  
The AI Perception Component is a type of Component thatcan be added to a Pawn's Blueprint from the Components window and is used to define what senses to listen for, the parameters for those senses, and how to respond when a sense has been detected. You can also use several different functions to get information about what was sensed, what Actors were sensed, or even disable or enable a particular type of sense.
  
AI Perception Component는 Components 창에서 Pawn의 Blueprint에 추가 할 수있는 Component 유형으로, 데이터 수집을 원하는 감각과 해당 감각에 대한 매개 변수 및 감각이 감지 될 때 반응하는 방법을 정의하는 데 사용됩니다. 또한 여러 다른 기능을 사용하여 감지 된 것, 감지 된 행위자에 대한 정보를 얻거나 특정 유형의 감지를 비활성화 또는 활성화 할 수도 있습니다.
  
  
In addition to the common properties available with in the Details panel for the AI Perception Component, you can add the type of Senses to perceive under the AI Perception and Senses Config section. Depending on the type of Sense, different properties are available to adjust how the Sense is perceived.
  
AI Perception 구성 요소에 대한 세부 정보 패널에서 사용할 수있는 공통 속성 외에도 AI Perception and Senses Config 섹션에서 감지 할 감지 유형을 추가 할 수 있습니다. 감지 유형에 따라 감지 속성을 조정하기 위해 다양한 속성을 사용할 수 있습니다.
  
  
### Note
The Dominant Sense property can be used to assign a Sense that should take precedence over other senses when determining a sensed Actor's location. This should be set to one of the senses configured in your Senses Config section or set to None.
  
Dominant Sense 프로퍼티는 감지 된 액터의 위치를 ​​결정할 때 다른 감각보다 우선해야하는 감각을 할당하는 데 사용될 수 있습니다. 이것은 Senses Config 섹션에서 구성된 감각 중 하나로 설정되거나 None으로 설정되어야합니다.
  
  
### AI Damage
If you want your AI to react to damage events such as Event Any Damage , Event Point Damage , or Event Radial Damage , you can use the AI Damage Sense Config. The Implementation property (which defaults to the engine class AISense_Damage) can be used to determine how damage events are handled, however you can create your own damage classes through C++ code.
  
AI가 Event Any Damage, Event Point Damage 또는 Event Radial Damage와 같은 손상 이벤트에 반응하게하려면 AI Damage Sense Config를 사용할 수 있습니다. 구현 속성 (기본값은 엔진 클래스 AISense_Damage)을 사용하여 손상 이벤트 처리 방법을 결정할 수 있지만 C ++ 코드를 통해 고유 한 손상 클래스를 만들 수 있습니다.

Implementation  이 항목에 사용할 AI 감지 클래스
Debug Color     When using the AI Debugging tools, what color to draw the debug lines.
Max Age         Determines the duration in which the stimuli generated by this sense becomes forgotten (0 means never forgotten).
Starts Enabled  Determines whether the given sense starts in an enabled state or must be manually enabled/disabled.
  </br>
</br>
### AI Hearing
The AI Hearing sense can be use to detect sounds generated by a Report Noise Event, for example, a projectile hits something and generates a sound which can be registered with the AI Hearing sense.
  </br>
AI Hearing 센스는 Report Noise Event에 의해 생성 된 사운드를 감지하는 데 사용할 수 있습니다. 예를 들어, 발사체가 무언가를 치고 AI Hearing 센스에 등록 할 수있는 사운드를 생성합니다.
</br>
</br>
Implementation              The AI Sense Class to use for this entry (defaults to AISense_Hearing).
Hearing Range               The distance in which this sense can be perceived by the AI Perception system.
Lo SHearing Range           This is used to display a different radius in the debugger for Hearing Range.
Detection by Affiliation    Determines if Enemies, Neutrals, or Friendlies can trigger this sense.
Debug Color                 When using the AI Debugging tools, what color to draw the debug lines.
Max Age                     Determines the duration in which the stimuli generated by this sense becomes forgotten (0 means never forgotten).
Starts Enabled              Determines whether the given sense starts in an enabled state or must be manually enabled/disabled.
</br>
### AI Prediction
</br>
This asks the Perception System to supply Requestor with PredictedActor's predicted location in PredictionTime seconds.

이를 통해 Perception 시스템은 PredictionTime 초 내에 PredictedActor의 예상 위치를 요청자에게 제공하도록 요청합니다.

Debug Color                 When using the AI Debugging tools, what color to draw the debug lines.
Max Age                     Determines the duration in which the stimuli generated by this sense becomes forgotten (0 means never forgotten).
Starts Enabled              Determines whether the given sense starts in an enabled state or must be manually enabled/disabled.

</br>
### AI Sight
</br>
The AI Sight config enables you to define parameters that allow an AI character to "see" things in your Level. When an Actor enters the Sight Radius, the AI Perception System signals an update and passes through the Actor that was seen (for example a Player enters the radius and is perceived by the AI who has Sight Perception).

AI Sight 구성을 사용하면 AI 캐릭터가 레벨에서 사물을 "볼"수있는 매개 변수를 정의 할 수 있습니다. 액터가 시력 반경에 들어가면 AI Perception System은 업데이트 신호를 보내고 본 액터를 통과합니다 (예 : 플레이어가 반경에 들어가서 시력을 인식하는 AI에 의해 인식됨).

Implementation                          The AI Sense Class to use for this entry (defaults to AISense_Sight).

Sight Radius                            The max distance over which this sense can start perceiving.

Lose Sight Radius                       The max distance in which a seen target is no longer perceived by the sight sense.

Peripheral Vision Half Angle Degrees    How far to the side the AI can see in degrees. The value represents the angle measured in relation to the forward vector, not the whole range. You can use SetPeripheralVisionAngle in Blueprint to change the value at runtime.

Detection by Affiliation                Determines if Enemies, Neutrals, or Friendlies can trigger this sense. This property can be used to set up Sight perception for teams. Currently, Affiliation can only be defined in C++. For Blueprints, you can use the Detect Neutrals option to detect all Actors, then use Tags to filter out Actor types.

Auto Success Range from Last Seen Location  When greater than zero, the AI will always be able to see the a target that has already been seen as long as they are within the range specified here.

Debug Color                             When using the AI Debugging tools, what color to draw the debug lines.

Max Age                                 Determines the duration in which the stimuli generated by this sense becomes 
forgotten (0 means never forgotten).

Starts Enabled                          Determines whether the given sense starts in an enabled state or must be manually enabled/disabled.

</br>
### AI Team
</br>
This notifies the Perception component owner that someone on the same team is close by (radius is sent by the gameplay code which sends the event).

이것은 같은 팀의 누군가가 가까이에 있음을 Perception 컴포넌트 소유자에게 알립니다 (반경은 이벤트를 보내는 게임 플레이 코드에 의해 보내집니다).

Debug Color                 When using the AI Debugging tools, what color to draw the debug lines.

Max Age                     Determines the duration in which the stimuli generated by this sense becomes forgotten (0 means never forgotten).

Starts Enabled              Determines whether the given sense starts in an enabled state or must be manually enabled/disabled.

</br>
### AI Touch
</br>
The AI Touch config setting gives you the ability to detect when the AI bumps into something or something bumps into it. For example, in a stealth based game, you may want a Player to sneak by an enemy AI without touching them. Using this Sense you can determine when the Player touches the AI and can respond with different logic.

AI Touch 구성 설정을 사용하면 AI가 무언가 또는 무언가에 부딪 치는시기를 감지 할 수 있습니다. 예를 들어, 스텔스 기반 게임에서 플레이어가 적 AI에 닿지 않고 몰래 들어가기를 원할 수 있습니다. 이 Sense를 사용하면 플레이어가 AI를 터치하는 시점을 결정하고 다른 논리로 응답 할 수 있습니다.

Debug Color             When using the AI Debugging tools, what color to draw the debug lines.

Max Age                 Determines the duration in which the stimuli generated by this sense becomes forgotten (0 means never forgotten).

Starts Enabled          Determines whether the given sense starts in an enabled state or must be manually enabled/disabled.


### Perception Events
The Events section enables you to define what happens when the AI Perception System receives an update or when the AI Perception Component is activated or deactivated.

Events 섹션에서는 AI Perception System이 업데이트를 받거나 AI Perception 구성 요소가 활성화 또는 비활성화 될 때 발생하는 상황을 정의 할 수 있습니다.

On Perception Updated           이 이벤트는 Perception System이 업데이트를 수신하면 시작되고 업데이트를 알리는 액터 배열을 반환합니다.

On Target Perception Updated    이 이벤트는 Perception System이 업데이트를 받으면 시작되고 업데이트를 알리는 액터를 반환합니다. 또한 추가 정보를 검색하기 위해 분류 할 수있는 AI Stimulus 구조체를 반환합니다.

On Component Activated          An Event that is fired when the AI Perception Component is activated.

On Component Deactivated        An Event that is fired when the AI Perception Component is deactivated.


Perception Function Calls
The following functions can be called through Blueprint to get information from or affect the Perception System.
블루 프린트를 통해 다음 함수를 호출하여 Perception System에서 정보를 얻거나 영향을 줄 수 있습니다.

Get Actors Perception                Retrieves whatever has been sensed about a given Actor and returns a Sensed Actor's Data structure.

Get Currently Perceived Actors       Returns all Actors that are being perceived based on a given Sense. If no Sense is specified, all Actors currently perceived in any way will be returned.

Get Known Perceived Actors           Returns any Actors that have been perceived (and not yet forgotten) based on a given Sense. If no Sense is specified, all Actors that have been perceived will be returned.

Get Perceived Hostile Actors         Returns the list of Hostile Actors (any hostile Actors that had a stimulus sensed which is not expired or successfully sensed). Method can be overridden in Blueprint to return whatever Actors list the user wants.

Request Stimuli Listener Update      Manually forces the AI Perception System to update properties for the specified target stimuli listener.

Set Sense Enabled                    Enable or Disable the specified Sense Class.  This only works if the given Sense has already been configured for the target component instance.


### Stimuli Source

The AI Perception Stimuli Source Component gives the owning Actor a way to automatically register itself as a stimuli source for the designated Sense(s) within the Perception System. An example use case would be to have an AI character with an AI Perception Component set up to perceive stimuli based on Sight. You could then use the Stimuli Source Component in an Actor (such as an item pickup Actor) and register it as a stimuli for Sight (which would enable the AI to "see" the Actor in the Level).

AI Perception Stimuli Source Component는 소유 액터에게 Perception System 내의 지정된 Sense에 대한 자극 소스로 자동 등록하는 방법을 제공합니다. 사용 사례의 예로는 AI Perception Component가있는 AI 캐릭터가 Sight를 기반으로 자극을 인식하도록 설정하는 것입니다. 그런 다음 액터 (예 : 아이템 픽업 액터)에서 Stimuli Source Component를 사용하여 Sight의 자극으로 등록 할 수 있습니다 (AI가 레벨에서 액터를 "볼"수 있도록합니다).


Property

Auto Register as Source
Whether to automatically register the stimuli for the specified sense with respect to the owning Actor.

소유 액터에 대해 지정된 감각에 대한 자극을 자동으로 등록할지 여부.

Register as Source for Senses
An array of Senses to register as a source for. Click the + sign to add a Source, then click the drop-down and assign the desired Sense.
소스로 등록 할 감각 배열입니다. + 부호를 클릭하여 소스를 추가 한 다음 드롭 다운을 클릭하고 원하는 감지를 지정하십시오.

You can also assign any custom Senses that have been based on the AISense Class.
AISense 클래스를 기반으로 한 사용자 지정 감지를 할당 할 수도 있습니다.

### Stimuli Function Calls
The following functions can be called through Blueprint for the AI Perception Stimuli Source Component:
AI Perception Stimuli Source Component에 대한 블루 프린트를 통해 다음 함수를 호출 할 수 있습니다.

Register for Sense          Registers owning Actor as a stimuli source for the specified Sense class.

Register with Perception System :
Registers owning Actor as a stimuli source for Senses specified in the Register as Source for Senses property and through the Register for Sense function call.

You do not need to call this function if the Auto Register as Source property is enabled.

Unregister from Perception System :
Unregisters the owning Actor from being a source of Sense stimuli.

Unregister from Sense :
Unregisters the stimuli for the specified sense with respect to the owning Actor.

### AI Perception Debugging
You can debug AI Perception using the AI Debugging tools by pressing the '(apostrophe) key while your game is running, then pressing numpad key 4 to bring up the Perception information.

게임이 실행되는 동안 '(아포스트로피) 키를 누른 다음 숫자 키 4를 눌러 인식 정보를 표시하면 AI 디버깅 도구를 사용하여 AI 인식을 디버깅 할 수 있습니다.