# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-10-10T13:50:02.056316+09:00

### 次に取るべきアクション
> RED最優先: STRATEGY_CI_FAIL×17 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×45 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 PSI_DRIFT_DETECTED×16 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 PSI_DRIFT_DETECTED  ×24  [2026-10-10T13:26:38]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🔴 STRATEGY_CI_FAIL  ×47  [2026-10-10T13:03:36]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_ODDS_SHIFT  ×1  [2026-10-10T12:02:28]
- key: `ANOMALY_ODDS_SHIFT|`
- **FIX**: odds 分布が2σシフト。scraper format変化・市場変動・戦略filterレンジ変更

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×37  [2026-10-10T11:36:17]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×7  [2026-10-10T10:39:22]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_BET_VOLUME_DROP  ×60  [2026-10-10T10:00:08]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-10T06:00:24]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=81<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-10T06:00:24]
- key: `INSUFFICIENT_SAMPLE|S00: n=164<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-10T06:00:24]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=163<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-10-10T06:00:24]
- key: `ORPHAN_SCAN|170 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ ROI_STAT  ×1  [2026-10-10T06:00:24]
- key: `ROI_STAT|S00: n=164 hit%=26.8% hit_CI[Bonf]=[18.1,37.8]% ROI=0.70 ROI_boot95=[0.50,0.92]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-10T06:00:24]
- key: `ROI_STAT|S01_NAKAANA1: n=163 hit%=33.1% hit_CI[Bonf]=[23.5,44.4]% ROI=1.03 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-10T06:00:24]
- key: `ROI_STAT|S02_TETSUBAN: n=81 hit%=48.1% hit_CI[Bonf]=[33.1,63.6]% ROI=0.83 ROI_boot95=[0.6`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-10T06:00:24]
- key: `DRIFT_BUCKET|drift ≤-30%: n=29 hit%=44.8% ROI=1.23 (コスト 8,300/回収 10,170)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-10T06:00:24]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=51 hit%=29.4% ROI=0.73 (コスト 12,000/回収 8,780)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-10T06:00:24]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=88 hit%=33.0% ROI=0.88 (コスト 19,900/回収 17,610)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-10T06:00:24]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=48 hit%=37.5% ROI=0.81 (コスト 11,300/回収 9,160)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-10T06:00:24]
- key: `DRIFT_BUCKET|drift ≥+30%: n=42 hit%=23.8% ROI=0.72 (コスト 11,000/回収 7,920)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-10T06:00:24]
- key: `CALIBRATION_LIVE|bt=win: n=408 pred=0.4820 actual=0.3358 error=+0.1463 (+30%) brier=0.2509 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-10T06:00:24]
- key: `CALIBRATION_LIVE|S00(win): n=164 pred=0.4538 hit=0.2683 cal_err=+0.1855 brier=0.2527 BSS=-0.29 RO`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 15.36MB / last modified 2026-10-10T13:49:33.322267+09:00

### データファイル存在確認
| file | exists | md5 | size |
|---|---|---|---|
| lgbm_model_top1.txt | True | `5b55d55bdb59df95ccfd1745d4e9b469` | 769682 |
| lgbm_model_top3.txt | True | `d5fd8d8393fd859ed913813abbf60084` | 969111 |
| calibration_v7.json | True | `1c04ab3c1a1f074da889e6f5f06adbf3` | 1450 |
| pl_corr_v8_final.json | True | `8727224dfcc3d7548845e2e41caef7be` | 1209 |

### crontab
```
# boatrace_v2 - managed by めう/Claude
SHELL=/bin/bash
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

# 1分毎: 統合サイクル (run_cycle.py, flock で並行実行防止)
* 8-23 * * * cd /opt/boatrace_v2 && flock -n /var/lock/run_cycle.lock /opt/boatrace/venv/bin/python3 run_cycle.py >> logs/run_cycle.log 2>&1

# 10分毎: pending alert flush
*/10 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 dispatch_pending.py >> logs/dispatch.log 2>&1

# 10分毎: snapshot 生成 + GitHub 同期 (Claude 次セッション用)
*/10 * * * * cd /opt/boatrace_v2 && bash sync_snapshot_to_github.sh >> logs/sync_snapshot.log 2>&1

# 5分毎: 結果取得
*/5 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 record_results.py >> logs/results.log 2>&1

# 30分毎: health check
*/30 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 health.py >> logs/health.log 2>&1

# 6時: 日次総合検査
0 6 * * *  cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 verify_all.py >> logs/verify_all.log 2>&1

# 0時: 日次集計
5 0 * * *  cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 daily_summary.py >> logs/daily.log 2>&1
0 3 * * * find /opt -maxdepth 1 -name "boatrace_v2.bak_*" -mtime +7 -exec rm -rf {} \; # backup cleanup

# 30分毎: コード/DB a
```

### 直近 run_cycle ログ (末尾)
```
by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-10 13:49:04,086 [INFO] predictor: Models loaded OK
2026-10-10 13:49:15,476 [INFO] scraper: odds3t: 120/120 parsed
2026-10-10 13:49:16,624 [INFO] scraper: odds3f: 20/20 parsed
2026-10-10 13:49:17,716 [INFO] scraper: odds2t: 30/30 parsed
2026-10-10 13:49:17,717 [INFO] scraper: odds2f: 15/15 parsed
2026-10-10 13:49:18,871 [INFO] scraper: odds_win: 4/6 parsed
2026-10-10 13:49:18,872 [INFO] scraper: fetch_race 08/8: boats=6 odds=189/191
2026-10-10 13:49:18,875 [INFO] predictor: CALIBRATION_MODE=on
2026-10-10 13:49:18,875 [INFO] predictor: combos: {'win': 4, '2t': 30, '3t': 120}
2026-10-10 13:49:18,879 [INFO] run_cycle: fetched 08/8 [final]: 154 combos
2026-10-10 13:49:22,729 [INFO] scraper: odds3t: 120/120 parsed
2026-10-10 13:49:23,848 [INFO] scraper: odds3f: 20/20 parsed
2026-10-10 13:49:24,952 [INFO] scraper: odds2t: 30/30 parsed
2026-10-10 13:49:24,953 [INFO] scraper: odds2f: 15/15 parsed
2026-10-10 13:49:26,073 [INFO] scraper: odds_win: 5/6 parsed
2026-10-10 13:49:26,074 [INFO] scraper: fetch_race 03/7: boats=6 odds=190/191
2026-10-10 13:49:26,077 [INFO] predictor: CALIBRATION_MODE=on
2026-10-10 13:49:26,077 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-10-10 13:49:26,083 [INFO] run_cycle: fetched 03/7 [scan]: 155 combos
2026-10-10 13:49:29,651 [INFO] scraper: odds3t: 120/120 parsed
2026-10-10 13:49:30,766 [INFO] scraper: odds3f: 20/20 parsed
2026-10-10 13:49:31,918 [INFO] scraper: odds2t: 30/30 parsed
2026-10-10 13:49:31,919 [INFO] scraper: odds2f: 15/15 parsed
2026-10-10 13:49:33,021 [INFO] scraper: odds_win: 6/6 parsed
2026-10-10 13:49:33,021 [INFO] scraper: fetch_race 09/8: boats=6 odds=191/191
2026-10-10 13:49:33,024 [INFO] predictor: CALIBRATION_MODE=on
2026-10-10 13:49:33,024 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-10-10 13:49:33,028 [INFO] run_cycle: fetched 09/8 [scan]: 156 combos
2026-10-10 13:49:33,148 [INFO] run_cycle: run_cycle done: 0 notifications

```

## 戦略有効/無効一覧
| id | trust | bt | ev_th | pmin | enabled |
|---|---|---|---|---|---|
| S00 | S | win | 4.0 | 0.0 | True |
| S01_NAKAANA1 | A | win | 1.5 | 0.0 | True |
| S02_TETSUBAN | A | win | 1.0 | 0.0 | True |
| S03_NAKAANA4 | B | win | 1.0 | 0.0 | False |
| S04_SELL_3T | B | 3t | 1.0 | 0.0 | False |
| S05_2T_MANKEN | B | 2t | 1.0 | 0.0 | False |
| S06_2F_AXIS1 | B | 2f | 1.0 | 0.0 | False |
| S07_2T_HONMEI | B | 2t | 1.0 | 0.0 | False |

## Webhook送信 (24h)
```
[
  {
    "target": "mirror",
    "ok": 1,
    "c": 61
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 61
  }
]
```

## Phase別通知記録 (24h)
{'final': 26, 'result': 12, 'scan': 23}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 129
  FINAL_MISSING: 45
  STRATEGY_CI_FAIL: 17
  PSI_DRIFT_DETECTED: 16
  ANOMALY_SCAN_FINAL_RATIO: 2
  ANOMALY_BET_VOLUME_DROP: 1
  ANOMALY_ODDS_SHIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 36 | 15 | 10,800 | 10,080 | -720 | 0.933 |
| S01_NAKAANA1 | 43 | 20 | 8,600 | 11,140 | +2,540 | 1.295 |
| S02_TETSUBAN | 14 | 5 | 2,800 | 1,620 | -1,180 | 0.579 |

## 直近アラート (24h・新しい順)
```
[13:48:31] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 312, "n_recent": 93, "psi": 0.321}
[13:26:38] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 311, "n_recent": 94, "psi": 0.312}
[13:23:21] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 312, "n_recent": 93, "psi": 0.308}
[13:03:36] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[12:49:33] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 312, "n_recent": 92, "psi": 0.315}
[12:32:33] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 313, "n_recent": 92, "psi": 0.316}
[12:28:27] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 314, "n_recent": 92, "psi": 0.317}
[12:27:22] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 315, "n_recent": 92, "psi": 0.349}
[12:25:20] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1132}
[12:23:25] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1142}
```

## 本日残レース: 89件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 156件 登録 / 67件 締切済
- 通知発射: scan=11 nid / final=14 nid / result=6 nid
- predictions: 9 / うち結果DB記録済: 7
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- ✅ scan後final無しのまま締切: 0件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 036R | win | 1 | 0.3177 | 5.7 | 1.81 | 300 | scan=4.6 drift=+23.9% | 13:26:29 |
| S01_NAKAANA1 | 097R | win | 1 | 0.4111 | 4.4 | 1.81 | 200 | scan=4.3 drift=+2.3% | 13:23:19 |
| S00 | 224R | win | 1 | 0.6040 | 4.6 | 2.78 | 300 | scan=9.0 drift=-48.9% | 12:27:19 |
| S01_NAKAANA1 | 239R | win | 1 | 0.5719 | 4.3 | 2.46 | 200 | scan=- drift=- | 12:19:29 |
| S01_NAKAANA1 | 223R | win | 1 | 0.5891 | 4.6 | 2.71 | 200 | scan=- drift=- | 12:03:29 |
| S00 | 223R | win | 1 | 0.5891 | 20.0 | 11.78 | 300 | scan=15.0 drift=+33.3% | 12:02:18 |
| S00 | 163R | win | 1 | 0.5174 | 6.7 | 3.47 | 300 | scan=- drift=- | 11:46:19 |
| S00 | 022R | win | 1 | 0.4111 | 13.2 | 5.43 | 300 | scan=4.1 drift=+222.0% | 11:13:19 |
| S01_NAKAANA1 | 186R | win | 1 | 0.5123 | 3.9 | 2.00 | 200 | scan=- drift=- | 11:00:33 |
| S02_TETSUBAN | 078R | win | 1 | 0.5735 | 2.4 | 1.38 | 200 | scan=- drift=- | 18:22:31 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 60 | +3.7% | -68.9% | +222.0% | 21 | 7 | 42 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 466.5s |
| **Latency** (scan→final max) | 611.6s |
| **Traffic** (notifications 24h) | 61 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 1,500円 used |
| **Saturation** (S01_NAKAANA1) | 800円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 403 | 0.4834 | 0.3400 | +0.1435 | 🟡+30% | 0.2524 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 165 | 0.4566 | 0.2667 | 0.2548 | 🔴-0.30 | 0.693 |
| S01_NAKAANA1 | win | 161 | 0.4927 | 0.3416 | 0.2468 | 🔴-0.10 | 1.049 |
| S02_TETSUBAN | win | 77 | 0.5215 | 0.4935 | 0.2589 | 🔴-0.04 | 0.853 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.30-0.50 | 150 | 0.4213 | 0.3067 | 🔴+0.1147 |
| 0.50+ | 239 | 0.5427 | 0.3598 | 🔴+0.1829 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 172 | 0.768 |
| win | <5.0 | ✅learned | 314 | 0.76 |
| win | <10.0 | ✅learned | 137 | 0.455 |
| win | <20.0 | ✅learned | 39 | 0.243 |
| win | <50.0 | ⚠️fallback | 8 | 0.1 |
| win | ∞ | ⚠️fallback | 0 | 0.1 |
| 2t | <10.0 | ⚠️fallback | 0 | 0.5 |
| 2t | <30.0 | ⚠️fallback | 0 | 0.35 |
| 2t | ∞ | ⚠️fallback | 0 | 0.25 |
| 3t | <10.0 | ⚠️fallback | 1 | 0.4 |
| 3t | <50.0 | ⚠️fallback | 0 | 0.4 |
| 3t | <200.0 | ⚠️fallback | 0 | 0.3 |
| 3t | ∞ | ⚠️fallback | 0 | 0.2 |
| 2f | <10.0 | ⚠️fallback | 0 | 0.45 |
| 2f | ∞ | ⚠️fallback | 0 | 0.3 |
| 3f | <50.0 | ⚠️fallback | 0 | 0.4 |
| 3f | ∞ | ⚠️fallback | 0 | 0.25 |

---
_auto-generated by claude_snapshot.py at 2026-10-10T13:50:02.056316+09:00_