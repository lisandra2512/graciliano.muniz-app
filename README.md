# graciliano.muniz-app
import { Dialog, DialogContent, DialogHeader, DialogTitle } from "@/components/ui/dialog";
import { Button } from "@/components/ui/button";
import { CheckCircle } from "lucide-react";
import { motion } from "framer-motion";
import { useState, useEffect } from "react";
import Confetti from "react-confetti";
import { useWindowSize } from "react-use";

export function MaterialSolicitation() {
  const [openConfirm, setOpenConfirm] = useState(false);
  const [showConfetti, setShowConfetti] = useState(false);
  const { width, height } = useWindowSize();

  const handleSolicitationSubmit = () => {
    setOpenConfirm(true);
    setShowConfetti(true);

    // Para o confete depois de 5 segundos
    setTimeout(() => {
      setShowConfetti(false);
    }, 5000);
  };

  return (
    <div className="flex flex-col gap-4 p-4">
      <Button onClick={handleSolicitationSubmit} className="w-full">
        Enviar Solicitação
      </Button>

      <Dialog open={openConfirm} onOpenChange={setOpenConfirm}>
        <DialogContent className="text-center flex flex-col items-center gap-4">
          {showConfetti && <Confetti width={width} height={height} numberOfPieces={300} />}

          <DialogHeader>
            <DialogTitle className="text-green-600 text-2xl">
              Solicitação Enviada!
            </DialogTitle>
          </DialogHeader>

          <motion.div
            initial={{ scale: 0 }}
            animate={{ scale: 1 }}
            transition={{ type: "spring", stiffness: 300 }}
          >
            <CheckCircle className="h-16 w-16 text-green-500" />
          </motion.div>

          <p className="text-muted-foreground">
            Sua solicitação foi registrada com sucesso.<br />
            Entraremos em contato em breve.
          </p>

          <Button onClick={() => setOpenConfirm(false)} className="mt-2">
            OK
          </Button>
        </DialogContent>
      </Dialog>
    </div>
  );
}
