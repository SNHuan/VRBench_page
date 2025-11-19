<script setup>
import InteractiveChart from './InteractiveChart.vue'

const MazeTypeGeneralizationData = {
  "DifficultyGeneralization": {
    "Base": {
      "EM": {
        "Easy":  { "baseline": 0.0,  "fine": 0.0,  "delta": 0.0 },
        "Med":   { "baseline": 0.0,  "fine": 4.2,  "delta": 4.2 },
        "Hard":  { "baseline": 0.0,  "fine": 0.0,  "delta": 0.0 }
      },
      "SR": {
        "Easy":  { "baseline": 8.3,  "fine": 83.3, "delta": 75.0 },
        "Med":   { "baseline": 8.3,  "fine": 41.7, "delta": 33.4 },
        "Hard":  { "baseline": 4.2,  "fine": 58.3, "delta": 54.1 }
      },
      "PR": {
        "Easy":  { "baseline": 13.2, "fine": 40.1, "delta": 26.9 },
        "Med":   { "baseline": 3.8,  "fine": 26.1, "delta": 22.3 },
        "Hard":  { "baseline": 2.7,  "fine": 6.0,  "delta": 3.3 }
      },
      "SD": {
        "Easy":  { "baseline": 154.8, "fine": 28.2, "delta": -126.6 },
        "Med":   { "baseline": null,  "fine": 10.1, "delta": null },
        "Hard":  { "baseline": null,  "fine": null, "delta": null }
      }
    },
    "Irrg": {
      "EM": {
        "Easy":  { "baseline": 0.0, "fine": 83.3, "delta": 83.3 },
        "Med":   { "baseline": 0.0, "fine": 66.7, "delta": 66.7 },
        "Hard":  { "baseline": 0.0, "fine": 54.2, "delta": 54.2 }
      },
      "SR": {
        "Easy":  { "baseline": 29.2, "fine": 95.8, "delta": 66.6 },
        "Med":   { "baseline": 4.2,  "fine": 87.5, "delta": 83.3 },
        "Hard":  { "baseline": 4.2,  "fine": 62.5, "delta": 58.3 }
      },
      "PR": {
        "Easy":  { "baseline": 13.4, "fine": 88.0, "delta": 74.6 },
        "Med":   { "baseline": 8.1,  "fine": 74.8, "delta": 66.7 },
        "Hard":  { "baseline": 5.8,  "fine": 68.4, "delta": 62.6 }
      },
      "SD": {
        "Easy":  { "baseline": 48.3, "fine": 3.5, "delta": -44.8 },
        "Med":   { "baseline": null, "fine": 7.8, "delta": null },
        "Hard":  { "baseline": 39.3, "fine": 3.1, "delta": -36.2 }
      }
    },
    "Trap": {
      "EM": {
        "Easy":  { "baseline": 0.0, "fine": 62.5, "delta": 62.5 },
        "Med":   { "baseline": 0.0, "fine": 0.0,  "delta": 0.0 },
        "Hard":  { "baseline": 0.0, "fine": 12.5, "delta": 12.5 }
      },
      "SR": {
        "Easy":  { "baseline": 0.0, "fine": 100.0, "delta": 100.0 },
        "Med":   { "baseline": 0.0, "fine": 95.8,  "delta": 95.8 },
        "Hard":  { "baseline": 0.0, "fine": 62.5,  "delta": 62.5 }
      },
      "PR": {
        "Easy":  { "baseline": 6.0, "fine": 86.7, "delta": 80.7 },
        "Med":   { "baseline": 6.4, "fine": 43.7, "delta": 37.3 },
        "Hard":  { "baseline": 8.9, "fine": 56.7, "delta": 47.8 }
      },
      "SD": {
        "Easy":  { "baseline": null, "fine": 2.1, "delta": null },
        "Med":   { "baseline": null, "fine": 5.9, "delta": null },
        "Hard":  { "baseline": null, "fine": 3.5, "delta": null }
      }
    },
    "3D": {
      "EM": {
        "Easy":  { "baseline": 0.0, "fine": 41.7, "delta": 41.7 },
        "Med":   { "baseline": 0.0, "fine": 0.0,  "delta": 0.0 },
        "Hard":  { "baseline": 0.0, "fine": 4.2,  "delta": 4.2 }
      },
      "SR": {
        "Easy":  { "baseline": 54.2, "fine": 100.0, "delta": 45.8 },
        "Med":   { "baseline": 16.7, "fine": 79.2,  "delta": 62.5 },
        "Hard":  { "baseline": 25.0, "fine": 83.3,  "delta": 58.3 }
      },
      "PR": {
        "Easy":  { "baseline": 7.6, "fine": 78.7, "delta": 71.1 },
        "Med":   { "baseline": 9.8, "fine": 47.4, "delta": 37.6 },
        "Hard":  { "baseline": 15.2, "fine": 58.7, "delta": 43.5 }
      },
      "SD": {
        "Easy":  { "baseline": 53.0, "fine": 4.6,  "delta": -48.4 },
        "Med":   { "baseline": 87.9, "fine": 10.2, "delta": -77.7 },
        "Hard":  { "baseline": 33.6, "fine": 13.8, "delta": -19.8 }
      }
    },
    "Soko": {
      "EM": {
        "Easy":  { "baseline": 0.0, "fine": 4.2, "delta": 4.2 },
        "Med":   { "baseline": 0.0, "fine": 0.0, "delta": 0.0 },
        "Hard":  { "baseline": 0.0, "fine": 0.0, "delta": 0.0 }
      },
      "SR": {
        "Easy":  { "baseline": 20.8, "fine": 83.3, "delta": 62.5 },
        "Med":   { "baseline": 8.3,  "fine": 45.8, "delta": 37.5 },
        "Hard":  { "baseline": 4.2,  "fine": 33.3, "delta": 29.1 }
      },
      "PR": {
        "Easy":  { "baseline": 14.6, "fine": 62.2, "delta": 47.6 },
        "Med":   { "baseline": 8.3,  "fine": 12.5, "delta": 4.2 },
        "Hard":  { "baseline": 5.6,  "fine": 10.4, "delta": 4.8 }
      },
      "SD": {
        "Easy":  { "baseline": 354.2, "fine": 18.8, "delta": -335.4 },
        "Med":   { "baseline": 61.4,  "fine": 84.5, "delta": 23.1 },
        "Hard":  { "baseline": null,  "fine": 16.1, "delta": null }
      }
    }
  }
}

const FidelityData = {
  "Fidelity": {
    "GeneralVideoModel__Veo-3.1-fast": {
    "MF": {
      "Base":  { "baseline": null, "fine": 43.2, "delta": null },
      "Irreg": { "baseline": null, "fine": 86.3, "delta": null },
      "Trap":  { "baseline": null, "fine": 22.5, "delta": null },
      "3D":    { "baseline": null, "fine": 69.1, "delta": null },
      "Soko":  { "baseline": null, "fine": 63.5, "delta": null }
    },
    "VLM-Score": {
      "Base":  { "baseline": null, "fine": 0.8, "delta": null },
      "Irreg": { "baseline": null, "fine": 2.5, "delta": null },
      "Trap":  { "baseline": null, "fine": 1.1, "delta": null },
      "3D":    { "baseline": null, "fine": 1.7, "delta": null },
      "Soko":  { "baseline": null, "fine": 2.0, "delta": null }
    }
  },

  "GeneralVideoModel__Veo-3.1-pro": {
    "MF": {
      "Base":  { "baseline": null, "fine": 80.5, "delta": null },
      "Irreg": { "baseline": null, "fine": 89.3, "delta": null },
      "Trap":  { "baseline": null, "fine": 82.2, "delta": null },
      "3D":    { "baseline": null, "fine": 73.4, "delta": null },
      "Soko":  { "baseline": null, "fine": 95.8, "delta": null }
    },
    "VLM-Score": {
      "Base":  { "baseline": null, "fine": 2.5, "delta": null },
      "Irreg": { "baseline": null, "fine": 2.8, "delta": null },
      "Trap":  { "baseline": null, "fine": 1.5, "delta": null },
      "3D":    { "baseline": null, "fine": 2.0, "delta": null },
      "Soko":  { "baseline": null, "fine": 2.5, "delta": null }
    }
  },

  "GeneralVideoModel__Sora-2": {
    "MF": {
      "Base":  { "baseline": null, "fine": 96.5, "delta": null },
      "Irreg": { "baseline": null, "fine": 97.2, "delta": null },
      "Trap":  { "baseline": null, "fine": 97.2, "delta": null },
      "3D":    { "baseline": null, "fine": 95.4, "delta": null },
      "Soko":  { "baseline": null, "fine": 95.2, "delta": null }
    },
    "VLM-Score": {
      "Base":  { "baseline": null, "fine": 3.9, "delta": null },
      "Irreg": { "baseline": null, "fine": 4.1, "delta": null },
      "Trap":  { "baseline": null, "fine": 3.9, "delta": null },
      "3D":    { "baseline": null, "fine": 3.3, "delta": null },
      "Soko":  { "baseline": null, "fine": 3.2, "delta": null }
    }
  },

  "GeneralVideoModel__kling-v1": {
    "MF": {
      "Base":  { "baseline": null, "fine": 55.5, "delta": null },
      "Irreg": { "baseline": null, "fine": 73.8, "delta": null },
      "Trap":  { "baseline": null, "fine": 54.4, "delta": null },
      "3D":    { "baseline": null, "fine": 84.9, "delta": null },
      "Soko":  { "baseline": null, "fine": 72.9, "delta": null }
    },
    "VLM-Score": {
      "Base":  { "baseline": null, "fine": 1.4, "delta": null },
      "Irreg": { "baseline": null, "fine": 2.5, "delta": null },
      "Trap":  { "baseline": null, "fine": 1.9, "delta": null },
      "3D":    { "baseline": null, "fine": 2.8, "delta": null },
      "Soko":  { "baseline": null, "fine": 2.8, "delta": null }
    }
  },

  "GeneralVideoModel__Seedance-1.0-pro": {
    "MF": {
      "Base":  { "baseline": null, "fine": 87.7, "delta": null },
      "Irreg": { "baseline": null, "fine": 97.2, "delta": null },
      "Trap":  { "baseline": null, "fine": 64.3, "delta": null },
      "3D":    { "baseline": null, "fine": 86.3, "delta": null },
      "Soko":  { "baseline": null, "fine": 83.0, "delta": null }
    },
    "VLM-Score": {
      "Base":  { "baseline": null, "fine": 3.0, "delta": null },
      "Irreg": { "baseline": null, "fine": 3.8, "delta": null },
      "Trap":  { "baseline": null, "fine": 2.4, "delta": null },
      "3D":    { "baseline": null, "fine": 2.7, "delta": null },
      "Soko":  { "baseline": null, "fine": 3.2, "delta": null }
    }
  },

  "GeneralVideoModel__MiniMax-Hailuo-2.3": {
    "MF": {
      "Base":  { "baseline": null, "fine": 92.4, "delta": null },
      "Irreg": { "baseline": null, "fine": 93.4, "delta": null },
      "Trap":  { "baseline": null, "fine": 91.4, "delta": null },
      "3D":    { "baseline": null, "fine": 94.9, "delta": null },
      "Soko":  { "baseline": null, "fine": 93.3, "delta": null }
    },
    "VLM-Score": {
      "Base":  { "baseline": null, "fine": 3.5, "delta": null },
      "Irreg": { "baseline": null, "fine": 3.4, "delta": null },
      "Trap":  { "baseline": null, "fine": 3.2, "delta": null },
      "3D":    { "baseline": null, "fine": 3.7, "delta": null },
      "Soko":  { "baseline": null, "fine": 3.6, "delta": null }
    }
  },

  "OpenSource__Wan2.5-i2v-preview": {
    "MF": {
      "Base":  { "baseline": null, "fine": 69.2, "delta": null },
      "Irreg": { "baseline": null, "fine": 74.8, "delta": null },
      "Trap":  { "baseline": null, "fine": 70.6, "delta": null },
      "3D":    { "baseline": null, "fine": 82.7, "delta": null },
      "Soko":  { "baseline": null, "fine": 90.4, "delta": null }
    },
    "VLM-Score": {
      "Base":  { "baseline": null, "fine": 1.2, "delta": null },
      "Irreg": { "baseline": null, "fine": 1.8, "delta": null },
      "Trap":  { "baseline": null, "fine": 2.6, "delta": null },
      "3D":    { "baseline": null, "fine": 2.6, "delta": null },
      "Soko":  { "baseline": null, "fine": 2.9, "delta": null }
    }
  },
  "OpenSource__Wan2.2-TI2V-5B": {
    "MF": {
      "Base":  { "baseline": null, "fine": 85.5, "delta": null },
      "Irreg": { "baseline": null, "fine": 97.4, "delta": null },
      "Trap":  { "baseline": null, "fine": 83.7, "delta": null },
      "3D":    { "baseline": null, "fine": 94.7, "delta": null },
      "Soko":  { "baseline": null, "fine": 93.5, "delta": null }
    },
    "VLM-Score": {
      "Base":  { "baseline": null, "fine": 2.8, "delta": null },
      "Irreg": { "baseline": null, "fine": 3.1, "delta": null },
      "Trap":  { "baseline": null, "fine": 1.5, "delta": null },
      "3D":    { "baseline": null, "fine": 3.3, "delta": null },
      "Soko":  { "baseline": null, "fine": 3.1, "delta": null }
    }
  },
  "Ours__Wan-R1": {
    "MF": {
      "Base":  { "baseline": null, "fine": 91.2, "delta": null },
      "Irreg": { "baseline": null, "fine": 98.1, "delta": null },
      "Trap":  { "baseline": null, "fine": 93.3, "delta": null },
      "3D":    { "baseline": null, "fine": 95.7, "delta": null },
      "Soko":  { "baseline": null, "fine": 94.1, "delta": null }
    },
    "VLM-Score": {
      "Base":  { "baseline": null, "fine": 4.2, "delta": null },
      "Irreg": { "baseline": null, "fine": 4.3, "delta": null },
      "Trap":  { "baseline": null, "fine": 4.4, "delta": null },
      "3D":    { "baseline": null, "fine": 4.0, "delta": null },
      "Soko":  { "baseline": null, "fine": 4.1, "delta": null }
    }
  },
  "Ours__Wan2.2-TI2V-5B": {
    "MF": {
      "Base":  { "baseline": null, "fine": 91.2, "baseline": null },
      "Irreg": { "baseline": null, "fine": 98.1, "baseline": null },
      "Trap":  { "baseline": null, "fine": 93.3, "baseline": null },
      "3D":    { "baseline": null, "fine": 95.7, "baseline": null },
      "Soko":  { "baseline": null, "fine": 94.1, "baseline": null }
    },
    "VLM-Score": {
      "Base":  { "baseline": null, "fine": 3.1, "baseline": null },
      "Irreg": { "baseline": null, "fine": 3.3, "baseline": null },
      "Trap":  { "baseline": null, "fine": 2.0, "baseline": null },
      "3D":    { "baseline": null, "fine": 4.0, "baseline": null },
      "Soko":  { "baseline": null, "fine": 3.6, "baseline": null }
    }
  }
  }
}

const MainData = {
  "ModelComparison": { 
    "VLM__Gemini-2.5-pro": {
      "EM": {
        "Base":  { "baseline": null, "fine": 2.8,  "delta": null },
        "Irreg": { "baseline": null, "fine": 36.1, "delta": null },
        "Trap":  { "baseline": null, "fine": 13.9, "delta": null },
        "3D":    { "baseline": null, "fine": 2.8,  "delta": null },
        "Soko":  { "baseline": null, "fine": 25.0, "delta": null }
      },
      "SR": {
        "Base":  { "baseline": null, "fine": 4.2,  "delta": null },
        "Irreg": { "baseline": null, "fine": 37.5, "delta": null },
        "Trap":  { "baseline": null, "fine": 13.9, "delta": null },
        "3D":    { "baseline": null, "fine": 2.8,  "delta": null },
        "Soko":  { "baseline": null, "fine": 31.9, "delta": null }
      },
      "PR": {
        "Base":  { "baseline": null, "fine": 9.5,  "delta": null },
        "Irreg": { "baseline": null, "fine": 47.9, "delta": null },
        "Trap":  { "baseline": null, "fine": 57.6, "delta": null },
        "3D":    { "baseline": null, "fine": 19.4, "delta": null },
        "Soko":  { "baseline": null, "fine": 33.8, "delta": null }
      },
      "SD": {
        "Base":  { "baseline": null, "fine": 25.0, "delta": null },
        "Irreg": { "baseline": null, "fine": 1.9,  "delta": null },
        "Trap":  { "baseline": null, "fine": 0.0,  "delta": null },
        "3D":    { "baseline": null, "fine": 0.0,  "delta": null },
        "Soko":  { "baseline": null, "fine": 1.1,  "delta": null }
      }
    },

    "VLM__Gpt-5-high": {
      "EM": {
        "Base":  { "baseline": null, "fine": 13.9, "delta": null },
        "Irreg": { "baseline": null, "fine": 31.9, "delta": null },
        "Trap":  { "baseline": null, "fine": 18.1, "delta": null },
        "3D":    { "baseline": null, "fine": 0.0,  "delta": null },
        "Soko":  { "baseline": null, "fine": 23.6, "delta": null }
      },
      "SR": {
        "Base":  { "baseline": null, "fine": 69.4, "delta": null },
        "Irreg": { "baseline": null, "fine": 33.3, "delta": null },
        "Trap":  { "baseline": null, "fine": 27.8, "delta": null },
        "3D":    { "baseline": null, "fine": 1.4,  "delta": null },
        "Soko":  { "baseline": null, "fine": 34.7, "delta": null }
      },
      "PR": {
        "Base":  { "baseline": null, "fine": 11.8, "delta": null },
        "Irreg": { "baseline": null, "fine": 43.6, "delta": null },
        "Trap":  { "baseline": null, "fine": 53.7, "delta": null },
        "3D":    { "baseline": null, "fine": 23.7, "delta": null },
        "Soko":  { "baseline": null, "fine": 35.6, "delta": null }
      },
      "SD": {
        "Base":  { "baseline": null, "fine": 31.0, "delta": null },
        "Irreg": { "baseline": null, "fine": 2.1,  "delta": null },
        "Trap":  { "baseline": null, "fine": 6.9,  "delta": null },
        "3D":    { "baseline": null, "fine": 20.0, "delta": null },
        "Soko":  { "baseline": null, "fine": 0.5,  "delta": null }
      }
    },

    "VLM__Qwen2.5-VL-7B": {
      "EM": {
        "Base":  { "baseline": null, "fine": 0.0, "delta": null },
        "Irreg": { "baseline": null, "fine": 1.3, "delta": null },
        "Trap":  { "baseline": null, "fine": 0.0, "delta": null },
        "3D":    { "baseline": null, "fine": 0.0, "delta": null },
        "Soko":  { "baseline": null, "fine": 1.4, "delta": null }
      },
      "SR": {
        "Base":  { "baseline": null, "fine": 1.4, "delta": null },
        "Irreg": { "baseline": null, "fine": 6.9, "delta": null },
        "Trap":  { "baseline": null, "fine": 1.4, "delta": null },
        "3D":    { "baseline": null, "fine": 1.4, "delta": null },
        "Soko":  { "baseline": null, "fine": 2.8, "delta": null }
      },
      "PR": {
        "Base":  { "baseline": null, "fine": 6.5, "delta": null },
        "Irreg": { "baseline": null,"fine": 12.4,"delta": null },
        "Trap":  { "baseline": null,"fine": 14.3,"delta": null },
        "3D":    { "baseline": null,"fine": 11.3,"delta": null },
        "Soko":  { "baseline": null, "fine": 7.8, "delta": null }
      },
      "SD": {
        "Base":  { "baseline": null, "fine": 300.0, "delta": null },
        "Irreg": { "baseline": null,  "fine": 26.7,  "delta": null },
        "Trap":  { "baseline": null,  "fine": 66.7,  "delta": null },
        "3D":    { "baseline": null,  "fine": 80.0,  "delta": null },
        "Soko":  { "baseline": null,"fine": 1150.0,"delta": null }
      }
    },

    "VLM__Qwen2.5-VL-7B-SFT": {
      "EM": {
        "Base":  { "baseline": null, "fine": 12.5, "delta": null },
        "Irreg": { "baseline": null, "fine": 29.2, "delta": null },
        "Trap":  { "baseline": null, "fine": 22.2, "delta": null },
        "3D":    { "baseline": null, "fine": 31.9, "delta": null },
        "Soko":  { "baseline": null, "fine": 29.8, "delta": null }
      },
      "SR": {
        "Base":  { "baseline": null, "fine": 52.8, "delta": null },
        "Irreg": { "baseline": null, "fine": 34.7, "delta": null },
        "Trap":  { "baseline": null, "fine": 52.8, "delta": null },
        "3D":    { "baseline": null, "fine": 36.1, "delta": null },
        "Soko":  { "baseline": null, "fine": 37.5, "delta": null }
      },
      "PR": {
        "Base":  { "baseline": null, "fine": 32.5, "delta": null },
        "Irreg": { "baseline": null,"fine": 45.1,"delta": null },
        "Trap":  { "baseline": null,"fine": 71.6,"delta": null },
        "3D":    { "baseline": null,"fine": 59.3,"delta": null },
        "Soko":  { "baseline": null, "fine": 43.0, "delta": null }
      },
      "SD": {
        "Base":  { "baseline": null, "fine": 52.6, "delta": null },
        "Irreg": { "baseline": null,  "fine": 2.3,  "delta": null },
        "Trap":  { "baseline": null,  "fine": 11.3, "delta": null },
        "3D":    { "baseline": null,  "fine": 4.5,  "delta": null },
        "Soko":  { "baseline": null,"fine": 3.0,  "delta": null }
      }
    },

    "GeneralVideoModel__Veo-3.1-fast": {
      "EM": {
        "Base":  { "baseline": null, "fine": 0.0, "delta": null },
        "Irreg": { "baseline": null, "fine": 0.0, "delta": null },
        "Trap":  { "baseline": null, "fine": 0.0, "delta": null },
        "3D":    { "baseline": null, "fine": 0.0, "delta": null },
        "Soko":  { "baseline": null, "fine": 2.8, "delta": null }
      },
      "SR": {
        "Base":  { "baseline": null, "fine": 40.3, "delta": null },
        "Irreg": { "baseline": null, "fine": 36.1, "delta": null },
        "Trap":  { "baseline": null, "fine": 38.9, "delta": null },
        "3D":    { "baseline": null, "fine": 48.6, "delta": null },
        "Soko":  { "baseline": null, "fine": 43.1, "delta": null }
      },
      "PR": {
        "Base":  { "baseline": null, "fine": 20.2, "delta": null },
        "Irreg": { "baseline": null, "fine": 24.8, "delta": null },
        "Trap":  { "baseline": null, "fine": 28.2, "delta": null },
        "3D":    { "baseline": null, "fine": 13.4, "delta": null },
        "Soko":  { "baseline": null, "fine": 21.7, "delta": null }
      },
      "SD": {
        "Base":  { "baseline": null, "fine": 195.3, "delta": null },
        "Irreg": { "baseline": null, "fine": 111.5, "delta": null },
        "Trap":  { "baseline": null, "fine": 80.7,  "delta": null },
        "3D":    { "baseline": null, "fine": 33.5,  "delta": null },
        "Soko":  { "baseline": null, "fine": 112.3, "delta": null }
      }
    },

    "GeneralVideoModel__Veo-3.1-pro": {
      "EM": {
        "Base":  { "baseline": null, "fine": 0.0, "delta": null },
        "Irreg": { "baseline": null, "fine": 4.2, "delta": null },
        "Trap":  { "baseline": null, "fine": 1.4, "delta": null },
        "3D":    { "baseline": null, "fine": 0.0, "delta": null },
        "Soko":  { "baseline": null, "fine": 0.0, "delta": null }
      },
      "SR": {
        "Base":  { "baseline": null, "fine": 47.2, "delta": null },
        "Irreg": { "baseline": null, "fine": 36.1, "delta": null },
        "Trap":  { "baseline": null, "fine": 59.7, "delta": null },
        "3D":    { "baseline": null, "fine": 50.0, "delta": null },
        "Soko":  { "baseline": null, "fine": 37.5, "delta": null }
      },
      "PR": {
        "Base":  { "baseline": null, "fine": 24.6, "delta": null },
        "Irreg": { "baseline": null, "fine": 33.9, "delta": null },
        "Trap":  { "baseline": null, "fine": 39.1, "delta": null },
        "3D":    { "baseline": null, "fine": 18.0, "delta": null },
        "Soko":  { "baseline": null, "fine": 21.4, "delta": null }
      },
      "SD": {
        "Base":  { "baseline": null, "fine": 140.7, "delta": null },
        "Irreg": { "baseline": null, "fine": 94.5,  "delta": null },
        "Trap":  { "baseline": null, "fine": 85.4,  "delta": null },
        "3D":    { "baseline": null, "fine": 40.1,  "delta": null },
        "Soko":  { "baseline": null, "fine": 141.8, "delta": null }
      }
    },

    "GeneralVideoModel__Sora-2": {
      "EM": {
        "Base":  { "baseline": null, "fine": 1.4, "delta": null },
        "Irreg": { "baseline": null, "fine": 5.6, "delta": null },
        "Trap":  { "baseline": null, "fine": 0.0, "delta": null },
        "3D":    { "baseline": null, "fine": 0.0, "delta": null },
        "Soko":  { "baseline": null, "fine": 4.2, "delta": null }
      },
      "SR": {
        "Base":  { "baseline": null, "fine": 75.0, "delta": null },
        "Irreg": { "baseline": null, "fine": 72.2, "delta": null },
        "Trap":  { "baseline": null, "fine": 83.0, "delta": null },
        "3D":    { "baseline": null, "fine": 37.5, "delta": null },
        "Soko":  { "baseline": null, "fine": 43.1, "delta": null }
      },
      "PR": {
        "Base":  { "baseline": null, "fine": 45.1, "delta": null },
        "Irreg": { "baseline": null, "fine": 45.7, "delta": null },
        "Trap":  { "baseline": null, "fine": 46.6, "delta": null },
        "3D":    { "baseline": null, "fine": 19.3, "delta": null },
        "Soko":  { "baseline": null, "fine": 27.4, "delta": null }
      },
      "SD": {
        "Base":  { "baseline": null, "fine": 302.9, "delta": null },
        "Irreg": { "baseline": null, "fine": 187.0, "delta": null },
        "Trap":  { "baseline": null, "fine": 145.1, "delta": null },
        "3D":    { "baseline": null, "fine": 92.4,  "delta": null },
        "Soko":  { "baseline": null, "fine": 138.7, "delta": null }
      }
    },

    "GeneralVideoModel__kling-v1": {
      "EM": {
        "Base":  { "baseline": null, "fine": 0.0, "delta": null },
        "Irreg": { "baseline": null, "fine": 0.0, "delta": null },
        "Trap":  { "baseline": null, "fine": 0.0, "delta": null },
        "3D":    { "baseline": null, "fine": 0.0, "delta": null },
        "Soko":  { "baseline": null, "fine": 0.0, "delta": null }
      },
      "SR": {
        "Base":  { "baseline": null, "fine": 2.8,  "delta": null },
        "Irreg": { "baseline": null, "fine": 0.0,  "delta": null },
        "Trap":  { "baseline": null, "fine": 1.4,  "delta": null },
        "3D":    { "baseline": null, "fine": 27.8, "delta": null },
        "Soko":  { "baseline": null, "fine": 12.5, "delta": null }
      },
      "PR": {
        "Base":  { "baseline": null, "fine": 6.3,  "delta": null },
        "Irreg": { "baseline": null, "fine": 8.8,  "delta": null },
        "Trap":  { "baseline": null, "fine": 10.4, "delta": null },
        "3D":    { "baseline": null, "fine": 11.7, "delta": null },
        "Soko":  { "baseline": null, "fine": 9.0,  "delta": null }
      },
      "SD": {
        "Base":  { "baseline": null, "fine": 25.2,  "delta": null },
        "Irreg": { "baseline": null, "fine": null,  "delta": null },
        "Trap":  { "baseline": null, "fine": null,  "delta": null },
        "3D":    { "baseline": null, "fine": 69.7,  "delta": null },
        "Soko":  { "baseline": null, "fine": 356.1, "delta": null }
      }
    },

    "GeneralVideoModel__Seedance-1.0-pro": {
      "EM": {
        "Base":  { "baseline": null, "fine": 0.0, "delta": null },
        "Irreg": { "baseline": null, "fine": 2.8, "delta": null },
        "Trap":  { "baseline": null, "fine": 2.8, "delta": null },
        "3D":    { "baseline": null, "fine": 0.0, "delta": null },
        "Soko":  { "baseline": null, "fine": 0.0, "delta": null }
      },
      "SR": {
        "Base":  { "baseline": null, "fine": 75.0, "delta": null },
        "Irreg": { "baseline": null, "fine": 45.8, "delta": null },
        "Trap":  { "baseline": null, "fine": 59.7, "delta": null },
        "3D":    { "baseline": null, "fine": 77.8, "delta": null },
        "Soko":  { "baseline": null, "fine": 13.9, "delta": null }
      },
      "PR": {
        "Base":  { "baseline": null, "fine": 12.8, "delta": null },
        "Irreg": { "baseline": null, "fine": 35.8, "delta": null },
        "Trap":  { "baseline": null, "fine": 42.7, "delta": null },
        "3D":    { "baseline": null, "fine": 23.6, "delta": null },
        "Soko":  { "baseline": null, "fine": 17.1, "delta": null }
      },
      "SD": {
        "Base":  { "baseline": null, "fine": 162.3, "delta": null },
        "Irreg": { "baseline": null, "fine": 143.4, "delta": null },
        "Trap":  { "baseline": null, "fine": 99.1,  "delta": null },
        "3D":    { "baseline": null, "fine": 84.4,  "delta": null },
        "Soko":  { "baseline": null, "fine": 241.9, "delta": null }
      }
    },

    "GeneralVideoModel__MiniMax-Hailuo-2.3": {
      "EM": {
        "Base":  { "baseline": null, "fine": 0.0, "delta": null },
        "Irreg": { "baseline": null, "fine": 1.4, "delta": null },
        "Trap":  { "baseline": null, "fine": 2.8, "delta": null },
        "3D":    { "baseline": null, "fine": 0.0, "delta": null },
        "Soko":  { "baseline": null, "fine": 0.0, "delta": null }
      },
      "SR": {
        "Base":  { "baseline": null, "fine": 68.1, "delta": null },
        "Irreg": { "baseline": null, "fine": 40.3, "delta": null },
        "Trap":  { "baseline": null, "fine": 70.8, "delta": null },
        "3D":    { "baseline": null, "fine": 55.6, "delta": null },
        "Soko":  { "baseline": null, "fine": 45.8, "delta": null }
      },
      "PR": {
        "Base":  { "baseline": null, "fine": 23.2, "delta": null },
        "Irreg": { "baseline": null, "fine": 24.2, "delta": null },
        "Trap":  { "baseline": null, "fine": 30.3, "delta": null },
        "3D":    { "baseline": null, "fine": 20.3, "delta": null },
        "Soko":  { "baseline": null, "fine": 15.5, "delta": null }
      },
      "SD": {
        "Base":  { "baseline": null, "fine": 464.0, "delta": null },
        "Irreg": { "baseline": null, "fine": 170.0, "delta": null },
        "Trap":  { "baseline": null, "fine": 90.9,  "delta": null },
        "3D":    { "baseline": null, "fine": 50.1,  "delta": null },
        "Soko":  { "baseline": null, "fine": 165.5, "delta": null }
      }
    },

    "OpenSource__Wan2.5-i2v-preview": {
      "EM": {
        "Base":  { "baseline": null, "fine": 0.0, "delta": null },
        "Irreg": { "baseline": null, "fine": 2.8, "delta": null },
        "Trap":  { "baseline": null, "fine": 4.2, "delta": null },
        "3D":    { "baseline": null, "fine": 0.0, "delta": null },
        "Soko":  { "baseline": null, "fine": 0.0, "delta": null }
      },
      "SR": {
        "Base":  { "baseline": null, "fine": 58.3, "delta": null },
        "Irreg": { "baseline": null, "fine": 26.4, "delta": null },
        "Trap":  { "baseline": null, "fine": 77.8, "delta": null },
        "3D":    { "baseline": null, "fine": 24.5, "delta": null },
        "Soko":  { "baseline": null, "fine": 22.4, "delta": null }
      },
      "PR": {
        "Base":  { "baseline": null, "fine": 14.3, "delta": null },
        "Irreg": { "baseline": null, "fine": 21.8, "delta": null },
        "Trap":  { "baseline": null, "fine": 34.4, "delta": null },
        "3D":    { "baseline": null, "fine": 24.5, "delta": null },
        "Soko":  { "baseline": null, "fine": 17.1, "delta": null }
      },
      "SD": {
        "Base":  { "baseline": null, "fine": 378.4, "delta": null },
        "Irreg": { "baseline": null, "fine": 281.8, "delta": null },
        "Trap":  { "baseline": null, "fine": 73.2,  "delta": null },
        "3D":    { "baseline": null, "fine": 119.9, "delta": null },
        "Soko":  { "baseline": null, "fine": 278.0, "delta": null }
      }
    },

    "OpenSource__Wan2.2-TI2V-5B": {
      "EM": {
        "Base":  { "baseline": null, "fine": 0.0, "delta": null },
        "Irreg": { "baseline": null, "fine": 0.0, "delta": null },
        "Trap":  { "baseline": null, "fine": 0.0, "delta": null },
        "3D":    { "baseline": null, "fine": 0.0, "delta": null },
        "Soko":  { "baseline": null, "fine": 0.0, "delta": null }
      },
      "SR": {
        "Base":  { "baseline": null,  "fine": 6.9,  "delta": null },
        "Irreg": { "baseline": null, "fine": 12.5, "delta": null },
        "Trap":  { "baseline": null,  "fine": 0.0,  "delta": null },
        "3D":    { "baseline": null, "fine": 31.9, "delta": null },
        "Soko":  { "baseline": null, "fine": 11.1, "delta": null }
      },
      "PR": {
        "Base":  { "baseline": null,  "fine": 6.6,  "delta": null },
        "Irreg": { "baseline": null,  "fine": 9.1,  "delta": null },
        "Trap":  { "baseline": null,  "fine": 7.1,  "delta": null },
        "3D":    { "baseline": null, "fine": 12.8, "delta": null },
        "Soko":  { "baseline": null,  "fine": 9.2,  "delta": null }
      },
      "SD": {
        "Base":  { "baseline": null, "fine": 388.7, "delta": null },
        "Irreg": { "baseline": null,  "fine": 66.1,  "delta": null },
        "Trap":  { "baseline": null,  "fine": null,  "delta": null },
        "3D":    { "baseline": null,   "fine": 5.4,   "delta": null },
        "Soko":  { "baseline": null, "fine": 176.6, "delta": null }
      }
    },

    "Ours__Wan-R1": {
      "EM": {
        "Base":  { "baseline": null, "fine": 33.3, "delta": null },
        "Irreg": { "baseline": null, "fine": 56.9, "delta": null },
        "Trap":  { "baseline": null, "fine": 38.9, "delta": null },
        "3D":    { "baseline": null, "fine": 65.3, "delta": null },
        "Soko":  { "baseline": null, "fine": 4.2,  "delta": null }
      },
      "SR": {
        "Base":  { "baseline": null,  "fine": 76.4, "delta": null },
        "Irreg": { "baseline": null, "fine": 69.4, "delta": null },
        "Trap":  { "baseline": null,  "fine": 100.0,"delta": null },
        "3D":    { "baseline": null, "fine": 100.0,"delta": null },
        "Soko":  { "baseline": null, "fine": 69.4, "delta": null }
      },
      "PR": {
        "Base":  { "baseline": null,  "fine": 60.6, "delta": null },
        "Irreg": { "baseline": null,  "fine": 71.6, "delta": null },
        "Trap":  { "baseline": null,  "fine": 79.1, "delta": null },
        "3D":    { "baseline": null, "fine": 93.5, "delta": null },
        "Soko":  { "baseline": null,  "fine": 44.3, "delta": null }
      },
      "SD": {
        "Base":  { "baseline": null, "fine": 10.3, "delta": null },
        "Irreg": { "baseline": null,  "fine": 2.4,  "delta": null },
        "Trap":  { "baseline": null,  "fine": 3.9,  "delta": null },
        "3D":    { "baseline": null,   "fine": 3.9,  "delta": null },
        "Soko":  { "baseline": null, "fine": 10.2, "delta": null }
      }
    }
  }
}

const DifficultyGeneralizationData = {
  "DifficultyGeneralization": {
    "Baseline__Wan2.2-TI2V-5B": {
      "EM": {
        "Base":  { "baseline": null, "fine": 0.0, "delta": null },
        "Irreg": { "baseline": null, "fine": 0.0, "delta": null },
        "Trap":  { "baseline": null, "fine": 0.0, "delta": null },
        "3D":    { "baseline": null, "fine": 0.0, "delta": null },
        "Soko":  { "baseline": null, "fine": 0.0, "delta": null }
      },
      "SR": {
        "Base":  { "baseline": null, "fine": 6.9, "delta": null },
        "Irreg": { "baseline": null, "fine": 12.5, "delta": null },
        "Trap":  { "baseline": null, "fine": 0.0, "delta": null },
        "3D":    { "baseline": null, "fine": 31.9, "delta": null },
        "Soko":  { "baseline": null, "fine": 11.1, "delta": null }
      },
      "PR": {
        "Base":  { "baseline": null, "fine": 6.6, "delta": null },
        "Irreg": { "baseline": null, "fine": 9.1, "delta": null },
        "Trap":  { "baseline": null, "fine": 7.1, "delta": null },
        "3D":    { "baseline": null, "fine": 12.8, "delta": null },
        "Soko":  { "baseline": null, "fine": 9.2, "delta": null }
      },
      "SD": {
        "Base":  { "baseline": null, "fine": 388.7, "delta": null },
        "Irreg": { "baseline": null, "fine": 66.1, "delta": null },
        "Trap":  { "baseline": null, "fine": null, "delta": null },
        "3D":    { "baseline": null, "fine": 5.4, "delta": null },
        "Soko":  { "baseline": null, "fine": 176.6, "delta": null }
      }
    },

    "Finetune__Regular-Maze": {
      "EM": {
        "Base":  { "baseline": 0.0, "fine": 33.3, "delta": 33.3 },
        "Irreg": { "baseline": 0.0, "fine": 5.6,  "delta": 5.6 },
        "Trap":  { "baseline": 0.0, "fine": 1.4,  "delta": 1.4 },
        "3D":    { "baseline": 0.0, "fine": 0.0,  "delta": 0.0 },
        "Soko":  { "baseline": 0.0, "fine": 0.0,  "delta": 0.0 }
      },
      "SR": {
        "Base":  { "baseline": 6.9,  "fine": 76.4, "delta": 69.5 },
        "Irreg": { "baseline": 12.5, "fine": 8.3,  "delta": -4.2 },
        "Trap":  { "baseline": 0.0,  "fine": 88.9, "delta": 88.9 },
        "3D":    { "baseline": 31.9, "fine": 69.4, "delta": 37.5 },
        "Soko":  { "baseline": 11.1, "fine": 30.6, "delta": 19.5 }
      },
      "PR": {
        "Base":  { "baseline": 6.6,  "fine": 60.6, "delta": 54.0 },
        "Irreg": { "baseline": 9.1,  "fine": 22.7, "delta": 13.6 },
        "Trap":  { "baseline": 7.1,  "fine": 25.2, "delta": 18.1 },
        "3D":    { "baseline": 12.8, "fine": 13.7, "delta": 0.9 },
        "Soko":  { "baseline": 9.2,  "fine": 19.0, "delta": 9.8 }
      },
      "SD": {
        "Base":  { "baseline": 388.7, "fine": 10.3, "delta": -378.4 },
        "Irreg": { "baseline": 66.1,  "fine": 51.7, "delta": -14.4 },
        "Trap":  { "baseline": null,  "fine": 3.8,  "delta": null },
        "3D":    { "baseline": 5.4,   "fine": 12.7, "delta": 7.3 },
        "Soko":  { "baseline": 176.6, "fine": 49.3, "delta": -127.3 }
      }
    },

    "Finetune__Irregular-Maze": {
      "EM": {
        "Base":  { "baseline": 0.0, "fine": 0.0,  "delta": 0.0 },
        "Irreg": { "baseline": 0.0, "fine": 56.9, "delta": 56.9 },
        "Trap":  { "baseline": 0.0, "fine": 0.0,  "delta": 0.0 },
        "3D":    { "baseline": 0.0, "fine": 0.0,  "delta": 0.0 },
        "Soko":  { "baseline": 0.0, "fine": 0.0,  "delta": 0.0 }
      },
      "SR": {
        "Base":  { "baseline": 6.9,  "fine": 11.1, "delta": 4.2 },
        "Irreg": { "baseline": 12.5, "fine": 69.4, "delta": 56.9 },
        "Trap":  { "baseline": 0.0,  "fine": 52.8, "delta": 52.8 },
        "3D":    { "baseline": 31.9, "fine": 79.2, "delta": 47.3 },
        "Soko":  { "baseline": 11.1, "fine": 12.5, "delta": 1.4 }
      },
      "PR": {
        "Base":  { "baseline": 6.6,  "fine": 16.6, "delta": 10.0 },
        "Irreg": { "baseline": 9.1,  "fine": 71.6, "delta": 62.5 },
        "Trap":  { "baseline": 7.1,  "fine": 18.1, "delta": 11.0 },
        "3D":    { "baseline": 12.8, "fine": 16.8, "delta": 4.0 },
        "Soko":  { "baseline": 9.2,  "fine": 15.5, "delta": 6.3 }
      },
      "SD": {
        "Base":  { "baseline": 388.7, "fine": 35.8, "delta": -352.9 },
        "Irreg": { "baseline": 66.1,  "fine": 2.4,  "delta": -63.7 },
        "Trap":  { "baseline": null,  "fine": 6.9,  "delta": null },
        "3D":    { "baseline": 5.4,   "fine": 9.0,  "delta": 3.6 },
        "Soko":  { "baseline": 176.6, "fine": 40.7, "delta": -135.9 }
      }
    },

    "Finetune__3D-Maze": {
      "EM": {
        "Base":  { "baseline": 0.0, "fine": 0.0,  "delta": 0.0 },
        "Irreg": { "baseline": 0.0, "fine": 5.6,  "delta": 5.6 },
        "Trap":  { "baseline": 0.0, "fine": 0.0,  "delta": 0.0 },
        "3D":    { "baseline": 0.0, "fine": 65.3, "delta": 65.3 },
        "Soko":  { "baseline": 0.0, "fine": 0.0,  "delta": 0.0 }
      },
      "SR": {
        "Base":  { "baseline": 6.9,  "fine": 38.9, "delta": 32.0 },
        "Irreg": { "baseline": 12.5, "fine": 31.9, "delta": 19.4 },
        "Trap":  { "baseline": 0.0,  "fine": 30.6, "delta": 30.6 },
        "3D":    { "baseline": 31.9, "fine": 100.0,"delta": 68.1 },
        "Soko":  { "baseline": 11.1, "fine": 20.8, "delta": 9.7 }
      },
      "PR": {
        "Base":  { "baseline": 6.6,  "fine": 6.8,  "delta": 0.2 },
        "Irreg": { "baseline": 9.1,  "fine": 20.6, "delta": 11.5 },
        "Trap":  { "baseline": 7.1,  "fine": 6.7,  "delta": -0.4 },
        "3D":    { "baseline": 12.8, "fine": 93.5, "delta": 80.7 },
        "Soko":  { "baseline": 9.2,  "fine": 15.0, "delta": 5.8 }
      },
      "SD": {
        "Base":  { "baseline": 388.7, "fine": 108.2, "delta": -280.5 },
        "Irreg": { "baseline": 66.1,  "fine": 10.9,  "delta": -55.2 },
        "Trap":  { "baseline": null,  "fine": 8.8,   "delta": null },
        "3D":    { "baseline": 5.4,   "fine": 3.9,   "delta": -1.5 },
        "Soko":  { "baseline": 176.6, "fine": 80.6,  "delta": -96.0 }
      }
    },

    "Finetune__Sokoban": {
      "EM": {
        "Base":  { "baseline": 0.0, "fine": 0.0, "delta": 0.0 },
        "Irreg": { "baseline": 0.0, "fine": 1.4, "delta": 1.4 },
        "Trap":  { "baseline": 0.0, "fine": 1.4, "delta": 1.4 },
        "3D":    { "baseline": 0.0, "fine": 0.0, "delta": 0.0 },
        "Soko":  { "baseline": 0.0, "fine": 4.2, "delta": 4.2 }
      },
      "SR": {
        "Base":  { "baseline": 6.9,  "fine": 0.5,  "delta": -6.4 },
        "Irreg": { "baseline": 12.5, "fine": 22.2, "delta": 9.7 },
        "Trap":  { "baseline": 0.0,  "fine": 18.1, "delta": 18.1 },
        "3D":    { "baseline": 31.9, "fine": 22.2, "delta": -9.7 },
        "Soko":  { "baseline": 11.1, "fine": 69.4, "delta": 58.3 }
      },
      "PR": {
        "Base":  { "baseline": 6.6,  "fine": 15.7, "delta": 9.1 },
        "Irreg": { "baseline": 9.1,  "fine": 23.7, "delta": 14.6 },
        "Trap":  { "baseline": 7.1,  "fine": 36.2, "delta": 29.1 },
        "3D":    { "baseline": 12.8, "fine": 15.7, "delta": 2.9 },
        "Soko":  { "baseline": 9.2,  "fine": 44.3, "delta": 35.1 }
      },
      "SD": {
        "Base":  { "baseline": 388.7, "fine": 46.3, "delta": -342.4 },
        "Irreg": { "baseline": 66.1,  "fine": 34.4, "delta": -31.7 },
        "Trap":  { "baseline": null,  "fine": 39.9, "delta": null },
        "3D":    { "baseline": 5.4,   "fine": 20.1, "delta": 14.7 },
        "Soko":  { "baseline": 176.6, "fine": 10.2, "delta": -166.4 }
      }
    },

    "Finetune__Trapfield": {
      "EM": {
        "Base":  { "baseline": 0.0, "fine": 0.0,  "delta": 0.0 },
        "Irreg": { "baseline": 0.0, "fine": 0.0,  "delta": 0.0 },
        "Trap":  { "baseline": 0.0, "fine": 38.9, "delta": 38.9 },
        "3D":    { "baseline": 0.0, "fine": 0.0,  "delta": 0.0 },
        "Soko":  { "baseline": 0.0, "fine": 0.0,  "delta": 0.0 }
      },
      "SR": {
        "Base":  { "baseline": 6.9,  "fine": 93.1, "delta": 86.2 },
        "Irreg": { "baseline": 12.5, "fine": 40.3, "delta": 27.8 },
        "Trap":  { "baseline": 0.0,  "fine": 100.0,"delta": 100.0 },
        "3D":    { "baseline": 31.9, "fine": 79.2, "delta": 47.3 },
        "Soko":  { "baseline": 11.1, "fine": 6.9,  "delta": -4.2 }
      },
      "PR": {
        "Base":  { "baseline": 6.6,  "fine": 10.9, "delta": 4.3 },
        "Irreg": { "baseline": 9.1,  "fine": 12.9, "delta": 3.8 },
        "Trap":  { "baseline": 7.1,  "fine": 79.1, "delta": 72.0 },
        "3D":    { "baseline": 12.8, "fine": 14.7, "delta": 1.9 },
        "Soko":  { "baseline": 9.2,  "fine": 10.0, "delta": 0.8 }
      },
      "SD": {
        "Base":  { "baseline": 388.7, "fine": 57.5, "delta": -331.2 },
        "Irreg": { "baseline": 66.1,  "fine": 16.8, "delta": -49.3 },
        "Trap":  { "baseline": null,  "fine": 3.9,  "delta": null },
        "3D":    { "baseline": 5.4,   "fine": 11.4, "delta": 6.0 },
        "Soko":  { "baseline": 176.6, "fine": 57.8, "delta": -118.8 }
      }
    }
  }
}

const TextureGeneralizationData = {
    "TextureGeneralization": {
    "Base": {
      "EM": {
        "Raw":   { "baseline": 0.0,  "fine": 33.3, "delta": 33.3 },
        "Skin2": { "baseline": 0.0,  "fine": 1.4,  "delta": 1.4 },
        "Skin3": { "baseline": 0.0,  "fine": 23.6, "delta": 23.6 }
      },
      "SR": {
        "Raw":   { "baseline": 6.9,  "fine": 76.4, "delta": 69.5 },
        "Skin2": { "baseline": 4.2,  "fine": 38.9, "delta": 34.7 },
        "Skin3": { "baseline": 2.8,  "fine": 68.1, "delta": 65.3 }
      },
      "PR": {
        "Raw":   { "baseline": 6.6,  "fine": 60.6, "delta": 54.0 },
        "Skin2": { "baseline": 4.6,  "fine": 12.3, "delta": 7.7 },
        "Skin3": { "baseline": 9.4,  "fine": 51.0, "delta": 41.6 }
      },
      "SD": {
        "Raw":   { "baseline": 388.7, "fine": 10.3, "delta": -378.4 },
        "Skin2": { "baseline": 11.7,  "fine": 19.0, "delta": 7.3 },
        "Skin3": { "baseline": 14.9,  "fine": 9.0,  "delta": -5.9 }
      }
    },

    "Irreg": {
      "EM": {
        "Raw":   { "baseline": 0.0,  "fine": 56.9, "delta": 56.9 },
        "Skin2": { "baseline": 0.0,  "fine": 22.2, "delta": 22.2 },
        "Skin3": { "baseline": 0.0,  "fine": 15.3, "delta": 15.3 }
      },
      "SR": {
        "Raw":   { "baseline": 12.5, "fine": 69.4, "delta": 56.9 },
        "Skin2": { "baseline": 4.2,  "fine": 15.3, "delta": 11.1 },
        "Skin3": { "baseline": 2.1,  "fine": 23.6, "delta": 21.5 }
      },
      "PR": {
        "Raw":   { "baseline": 9.1,  "fine": 71.6, "delta": 62.5 },
        "Skin2": { "baseline": 12.0, "fine": 36.5, "delta": 24.5 },
        "Skin3": { "baseline": 47.8, "fine": 26.2, "delta": -21.6 }
      },
      "SD": {
        "Raw":   { "baseline": 66.1, "fine": 2.4, "delta": -63.7 },
        "Skin2": { "baseline": 39.5, "fine": 5.1, "delta": -34.4 },
        "Skin3": { "baseline": 42.0, "fine": 7.7, "delta": -34.3 }
      }
    },

    "3D": {
      "EM": {
        "Raw":   { "baseline": 0.0, "fine": 65.3, "delta": 65.3 },
        "Skin2": { "baseline": 0.0, "fine": 43.1, "delta": 43.1 },
        "Skin3": { "baseline": 0.0, "fine": 50.0, "delta": 50.0 }
      },
      "SR": {
        "Raw":   { "baseline": 0.0, "fine": 100.0, "delta": 100.0 },
        "Skin2": { "baseline": 4.2, "fine": 97.2,  "delta": 93.0 },
        "Skin3": { "baseline": 4.2, "fine": 100.0, "delta": 95.8 }
      },
      "PR": {
        "Raw":   { "baseline": 7.1, "fine": 93.5, "delta": 86.4 },
        "Skin2": { "baseline": 8.9, "fine": 83.8, "delta": 74.9 },
        "Skin3": { "baseline": 8.3, "fine": 86.8, "delta": 78.5 }
      },
      "SD": {
        "Raw":   { "baseline": null,  "fine": 3.9, "delta": null },
        "Skin2": { "baseline": 73.6,  "fine": 6.4, "delta": -67.2 },
        "Skin3": { "baseline": 59.3,  "fine": 5.9, "delta": -53.4 }
      }
    },

    "Soko": {
      "EM": {
        "Raw":   { "baseline": 0.0, "fine": 4.2, "delta": 4.2 },
        "Skin2": { "baseline": 0.0, "fine": 0.0, "delta": 0.0 },
        "Skin3": { "baseline": 0.0, "fine": 1.4, "delta": 1.4 }
      },
      "SR": {
        "Raw":   { "baseline": 31.9, "fine": 69.4, "delta": 37.5 },
        "Skin2": { "baseline": 2.8,  "fine": 34.7, "delta": 31.9 },
        "Skin3": { "baseline": 7.1,  "fine": 58.3, "delta": 51.2 }
      },
      "PR": {
        "Raw":   { "baseline": 12.8, "fine": 44.3, "delta": 31.5 },
        "Skin2": { "baseline": 9.3,  "fine": 21.0, "delta": 11.7 },
        "Skin3": { "baseline": 8.1,  "fine": 14.1, "delta": 6.0 }
      },
      "SD": {
        "Raw":   { "baseline": 5.4,  "fine": 10.2, "delta": 4.8 },
        "Skin2": { "baseline": null, "fine": 58.6, "delta": null },
        "Skin3": { "baseline": null, "fine": 82.6, "delta": null }
      }
    },

    "Trap": {
      "EM": {
        "Raw":   { "baseline": 0.0, "fine": 38.9, "delta": 38.9 },
        "Skin2": { "baseline": 0.0, "fine": 9.7,  "delta": 9.7 },
        "Skin3": { "baseline": 0.0, "fine": 0.0,  "delta": 0.0 }
      },
      "SR": {
        "Raw":   { "baseline": 11.1, "fine": 100.0, "delta": 88.9 },
        "Skin2": { "baseline": 0.0,  "fine": 38.9,  "delta": 38.9 },
        "Skin3": { "baseline": 0.0,  "fine": 1.4,   "delta": 1.4 }
      },
      "PR": {
        "Raw":   { "baseline": 9.2, "fine": 79.1, "delta": 69.9 },
        "Skin2": { "baseline": 9.0, "fine": 29.0, "delta": 20.0 },
        "Skin3": { "baseline": 7.5, "fine": 9.9,  "delta": 2.4 }
      },
      "SD": {
        "Raw":   { "baseline": 176.6, "fine": 3.9,  "delta": -172.7 },
        "Skin2": { "baseline": null,  "fine": 8.7,  "delta": null },
        "Skin3": { "baseline": null,  "fine": 18.5, "delta": null }
      }
    }
  }
}

const datasets = [
  {
    name: 'Main Data',
    data: MainData,
    caption: "Comparison of a diverse set of VLMs, closed-source video models, and open-source video generators across five maze-solving tasks (Base, Irreg, Trap, 3D, Soko). -- indicates that the model produced no successful cases for the corresponding task, making SD undefined."
  },
  {
    name: 'Fidelity Data',
    data: FidelityData,
    caption: "Comparison of closed-source and open-source video models across five maze-solving tasks (Base, Irreg, Trap, 3D, Soko). MF and VLM-Score denote Maze Fidelity and the rule-compliance score."
  }
]

const datasets_1 = [
  {
    name: 'Maze Type Generalization',
    data: MazeTypeGeneralizationData,
    caption: "Comparison between the baseline (Wan2.2-TI2V-5B) and task-specific fine-tuned models across five game types (Base, Irreg, Trap, 3D, Soko). Each cell reports absolute performance and relative change over the baseline on four metrics: EM, SR, PR, and SD. $\\textcolor{green}{Green}$ indicates improvement, $\\textcolor{red}{red}$ indicates degradation, and $\\textcolor{gray}{gray}$ denotes no change or undefined difference."
  },
  {
    name: 'Difficulty generalization',
    data: DifficultyGeneralizationData,
    caption: "Each task block compares the baseline (Wan2.2-TI2V-5B) and the fine-tuned model (trained only on Easy level) across difficulty levels (Easy, Medium, Hard) and four metrics (EM, SR, PR, SD). $\\textcolor{green}{Green}$ indicates improvement, $\\textcolor{red}{red}$ indicates degradation, and $\\textcolor{gray}{gray}$ denotes no change or undefined difference."
  },
  {
    name: 'Texture Generalization',
    data: TextureGeneralizationData,
    caption: "For each task, the table reports the baseline performance, the results after fine-tuning on the Raw texture, and the relative change across three texture conditions (Raw, Skin2, Skin3) on EM, SR, PR, and SD. $\\textcolor{green}{Green}$ indicates improvement, $\\textcolor{red}{red}$ indicates degradation, and $\\textcolor{gray}{gray}$ denotes no change or undefined difference."
  }
]



</script>

<template>
  <InteractiveChart :datasets="datasets" title="Main Result" />
  <InteractiveChart :datasets="datasets_1" title="Generalization Results" />
</template>
