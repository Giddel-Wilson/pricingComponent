<script lang="ts">
    import { Switch } from "$lib/components/ui/switch";
    import { Button } from "$lib/components/ui/button";
    import { Card } from "$lib/components/ui/card";
    import { Check } from "lucide-svelte";
    import background from '$lib/assets/bg-pattern.svg'
    import rounds from '$lib/assets/pattern-circles.svg'
    
    let pageviews = 100;
    let isYearly = false;
    let price = 16;
    
    $: displayPrice = isYearly ? (price * 0.75).toFixed(2) : price.toFixed(2);
    $: pageviewsDisplay = pageviews + 'K PAGEVIEWS';
    
    function updatePrice(value: number) {
      pageviews = value;
      price = (value / 6.25);
    }
  </script>
  
  <main class="min-h-screen w-full bg-[#F9FAFE] flex flex-col items-center justify-center">
    <div class="flex flex-col items-center justify-center p-4 relative z-20 py-16 md:py-0">
        <div class="text-center relative flex flex-col justify-center items-center mb-10 lg:mb-20">
          <h1 class="text-[#293356] text-2xl md:text-4xl font-extrabold mb-2 z-20">Simple, traffic-based pricing</h1>
          <p class="text-[#848693]">Sign-up for our 30-day trial. No credit card required.</p>
          <img src={rounds} alt="" class="absolute left-1/2 -translate-x-1/2 w-32 lg:w-[146px] -top-8 lg:-top-auto lg:h-[146px] bg-no-repeat z-10">
        </div>
      
        <Card class="w-full max-w-[540px] bg-white rounded-lg shadow-lg p-6 md:p-10">
          <div class="flex flex-col md:flex-row md:items-center md:justify-between mb-8">
            <p class="text-[#848693] uppercase tracking-wider text-sm font-bold text-center md:text-left">
              {pageviewsDisplay}
            </p>
            <div class="flex items-center justify-center md:justify-end gap-2 mt-4 md:mt-0">
              <span class="text-4xl font-extrabold text-[#293356]">${displayPrice}</span>
              <span class="text-[#848693]">/ month</span>
            </div>
          </div>
      
          <div class="mb-8">
            <input 
              type="range"
              min="0"
              max="200"
              step="50"
              bind:value={pageviews}
              on:input={(e) => updatePrice(Number(e.currentTarget.value))}
              class="w-full h-2 bg-[#ECF0FB] rounded-full appearance-none cursor-pointer"
            />
          </div>
      
          <div class="flex items-center justify-center gap-4 mb-8">
            <span class="text-[#848693]">Monthly Billing</span>
            <Switch
              checked={isYearly}
              onCheckedChange={(checked) => isYearly = checked}
              class="data-[state=checked]:bg-[#10D5C2] focus:border-none"
            />
            <div class="flex items-center gap-2">
              <span class="text-[#848693]">Yearly Billing</span>
              <span class="bg-[#FEECE7] text-[#FF8C66] text-xs font-bold px-2 py-1 rounded-full">
                -25%
              </span>
            </div>
          </div>
      
          <div class="border-t border-[#ECF0FB] pt-8">
            <div class="flex flex-col md:flex-row md:items-center md:justify-between gap-8">
              <ul class="space-y-3">
                <li class="flex items-center gap-4">
                  <Check class="w-4 h-4 text-[#10D5C2]" />
                  <span class="text-[#848693]">Unlimited websites</span>
                </li>
                <li class="flex items-center gap-4">
                  <Check class="w-4 h-4 text-[#10D5C2]" />
                  <span class="text-[#848693]">100% data ownership</span>
                </li>
                <li class="flex items-center gap-4">
                  <Check class="w-4 h-4 text-[#10D5C2]" />
                  <span class="text-[#848693]">Email reports</span>
                </li>
              </ul>
              
              <Button
                class="bg-[#293356] hover:bg-[#293356]/90 text-white rounded-full px-12 py-3"
              >
                Start my trial
              </Button>
            </div>
          </div>
        </Card>
      </div>
      <img src={background} alt="" class="absolute top-0 left-0 w-full h-96 md:h-[50vh] lg:h-[60vh] object-fill z-10">
  </main>
  
  <style>
    input[type="range"] {
      -webkit-appearance: none;
      appearance: none;
      background: transparent;
      cursor: pointer;
    }
  
    input[type="range"]::-webkit-slider-runnable-track {
      background: #ECF0FB;
      height: 8px;
      border-radius: 4px;
    }
  
    input[type="range"]::-webkit-slider-thumb {
      -webkit-appearance: none;
      appearance: none;
      margin-top: -16px;
      background-color: #10D5C2;
      height: 40px;
      width: 40px;
      border-radius: 50%;
      box-shadow: 0 10px 25px rgba(0, 255, 231, 0.6);
      cursor: pointer;
    }
  
    input[type="range"]::-webkit-slider-thumb:hover {
      background-color: #7AEADF;
    }
  
    input[type="range"]::-moz-range-track {
      background: #ECF0FB;
      height: 8px;
      border-radius: 4px;
    }
  
    input[type="range"]::-moz-range-thumb {
      border: none;
      background-color: #10D5C2;
      height: 40px;
      width: 40px;
      border-radius: 50%;
      box-shadow: 0 15px 30px rgba(0, 255, 231, 0.6);
      cursor: pointer;
    }
  
    input[type="range"]::-moz-range-thumb:hover {
      background-color: #7AEADF;
    }
  </style>
