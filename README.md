Cirkeluppgift
=============

package 
{
	import adobe.utils.CustomActions;
	import flash.automation.KeyboardAutomationAction;
	import flash.display.InteractiveObject;
	import flash.display.Sprite;
	import flash.events.DRMCustomProperties;
	import flash.events.Event;
	import flash.events.KeyboardEvent;
	import flash.events.MouseEvent;
	import flash.events.TextEvent;
	import flash.text.TextField;
	import flash.text.TextFormat;
	
	/**
	 * ...
	 * @author Sebastian Leijen
	 */
	public class Main extends Sprite 
	{
		private var score:int = 0;
		private const nr_circles:int = 20;
		private var cirkel:Vector.<Sprite> = new Vector.<Sprite>;
		private var text:TextField;  
		private var ondCirkel:Sprite = new Sprite;
		
		private function updateScore():void
		{
			text.text = "Score: " + score;
		}
		
		public function Main():void 
		{
			if (stage) init();
			else addEventListener(Event.ADDED_TO_STAGE, init);
		}
		
		
		private function ondCirkelKlick(e:MouseEvent):void
		{
			for (var i:int = 0; i < nr_circles; i++) 
			{
			cirkel[i].x = 8000;
			ondCirkel.visible = false;
			}
		}
		
		function clickCircle(e:MouseEvent):void
		{
			Sprite(e.target).visible = false;
			score ++;
			updateScore();
		}
			
function programStart(e:KeyboardEvent):void
{
	if (e.keyCode == 32)
	{
		score = 0;
	
			while (cirkel.length > 0)
			{
				removeChild(cirkel[0]);
				cirkel.shift();
			}
		
			for (var i:int = 0; i < nr_circles; i++) 
			{
				var circle:Sprite = new Sprite();
				circle.graphics.beginFill(0x0000ff);
				circle.graphics.drawCircle (0, 0, 30);
				circle.graphics.endFill();
				circle.x = Math.random() * 700+50;
				circle.y = Math.random() * 500+50;
				cirkel.push(circle);					
				addChild(circle);
				circle.addEventListener(MouseEvent.CLICK, clickCircle);
				
			}
			
			ondCirkel.graphics.beginFill(0x0000FF);
			ondCirkel.graphics.drawCircle (0, 0, 30);
			ondCirkel.graphics.endFill();
			ondCirkel.addEventListener (MouseEvent.CLICK, ondCirkelKlick);
			addChild(ondCirkel);
			ondCirkel.x = Math.random() * 700+50;
			ondCirkel.y = Math.random() * 50+50;
			}
		}
		
		
		function init(e:Event = null):void 
		{							
			removeEventListener(Event.ADDED_TO_STAGE, init);
			// entry point			
			
			stage.addEventListener(KeyboardEvent.KEY_DOWN, programStart);	
			text = new TextField();
			text.x = 50;
			score = 0;
			stage.addChild(text);
			updateScore();
		}
	}			
}			
