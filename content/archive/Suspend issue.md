echo "GP12" | sudo tee /proc/acpi/wakeup
echo "GP13" | sudo tee /proc/acpi/wakeup
echo "XHC0" | sudo tee /proc/acpi/wakeup
echo "GPP0" | sudo tee /proc/acpi/wakeup
echo "GPP8" | sudo tee /proc/acpi/wakeup
echo "PTXH" | sudo tee /proc/acpi/wakeup
echo "PT28" | sudo tee /proc/acpi/wakeup
echo "PT29" | sudo tee /proc/acpi/wakeup

Not this one most likely
echo XHC0 | sudo tee /proc/acpi/wakeup
